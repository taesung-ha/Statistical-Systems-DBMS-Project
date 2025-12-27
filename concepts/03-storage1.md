# CMU Intro to DB Systems - Lecture 03: Database Storage (Files, Pages, Tuples)

## 1. System Architecture Overview
A database system is structured as a series of layers with well-defined APIs. The focus of this session is the bottom-most layer: the Storage Manager.
- <strong>Storage Manager:</strong> Responsible for reading/writing data from the disk. It manages pages and identifies free space.
- <strong>Buffer Pool Manager:</strong> Sits above the storage manager, bringing pages into memory (DRAM) and ensuring they aren't swapped out while in use.
- <strong>Disk-Oriented Architecture:</strong> The system assumes the primary data location is non-volatile disk (SSD/HDD). Data must be moved to volatile memory (DRAM) to be operated upon.

## 2. Memory Hierarchy & Performance
The performance gap between different storage layers is massive.
- <strong>The Gap:</strong> Accessing DRAM takes ~100ns, while an SSD takes ~16,000ns+.
- <strong>Sequential vs. Random I/O:</strong> Sequential access is significantly faster than random access. Algorithms should be designed to maximize sequential strides and minimize random seeks to avoid system stalls.
- <strong>Design Goal:</strong> Manage a database larger than available memory by providing an "illusion" of infinite memory through clever paging.

## 3. Page Management
A database is essentially just files on disk, which the OS sees as normal files. The DBMS interprets these files as a collection of fixed-size <strong>Pages</strong>.
- <strong>Page Size:</strong> Common defaults include 4KB (SQLite, Oracle), 8KB (Postgres, SQL Server), or 16KB (MySQL). Larger pages are better for read-heavy scans; smaller pages are better for write-heavy random updates.
- <strong>Page Directory:</strong> A mapping layer that tracks where pages are located across files. This must be synchronized with disk pages to ensure recoverability.
- <strong>Heap File Organization:</strong> An unordered collection of pages where tuples are stored wherever there is free space.

## 4. Internal Page Layout (Slotted Pages)
To handle variable-length data and fragmentation, most systems use a <strong>Slotted Page</strong> architecture.
- <strong>Header:</strong> Contains metadata (checksum, page size, version, etc.).
- <strong>Slot Array:</strong> Located at the beginning of the page, growing downwards. It stores offsets to the actual tuple data.
- <strong>Tuple Data:</strong> Located at the end of the page, growing upwards.
- <strong>Indirection:</strong> Since the slot array points to the data, we can move or compact data within a page without updating indexes that point to the Record ID (PageID + Slot Index).

## 5. Tuple Structure & Data Representation
Tuples are essentially byte arrays with a header.
- <strong>Tuple Header:</strong> Contains visibility info (transactions) and a <strong>Null Bitmap</strong> to track which columns are null.
- <strong>Alignment:</strong> Attributes are padded (usually to 64-bit boundaries) to ensure fast hardware access and avoid compiler errors.
- <strong>Numeric Data:</strong> 
  - <strong>Floats/Doubles:</strong> Fast but imprecise (IEEE 754).
  - <strong>Fixed-Point (Numeric/Decimal):</strong> DBMS-managed (e.g., Postgres `numeric`). They store exact values using custom structs and logic, which is slower but critical for financial/scientific data.
- <strong>Large Values (Overflow):</strong> If a tuple exceeds a page size (or a threshold like 2KB), it is stored in <strong>Overflow Pages</strong> (Postgres calls this TOAST). The original tuple stores a pointer to these pages.

## 6. Key Takeaways for Project 1
- A DBMS is a collection of pages.
- The Buffer Manager (next topic) will be critical for managing the movement of these pages between disk and memory.
- Abstracting the storage details allows the rest of the system to operate without knowing the physical layout on disk.