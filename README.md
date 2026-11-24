PharmaStock
Pharmacy Inventory Management System
CS2003 – Data Structures & Business Applications

ABOUT THE PROJECT

PharmaStock is a desktop application for managing fictional pharmacy stock. It opens directly to the Inventory tab. All prices are in Pakistani rupees (PKR).

The application starts with 12 sample medicine batches. Changes stay available while the app is open. Closing and reopening the app resets the sample data.

FEATURES

1. Inventory – Add, edit, delete and search for medicines by name or ID.
2. Sales – Queue customer orders, process the next order and view sales revenue. The app rejects orders for expired medicines or insufficient stock.
3. Expiry – View medicines in order of expiry, with the earliest date first.
4. Low Stock – Find medicines with fewer than 10 units and restock them.
5. Suppliers – Explore supplier connections and find suppliers for low-stock medicines.
6. Sorting – Sort medicines by name, price or quantity. View the number of comparisons, swaps and time taken.

HOW TO RUN ON WINDOWS

1. Right-click PharmaStock-Source.zip and choose Extract All.
2. Install Visual Studio Build Tools 2022. Select “Desktop development with C++” during installation.
3. Install CMake 3.21 or newer. Select “Add CMake to PATH” during setup.
4. Open the extracted PharmaStock folder. You should see CMakeLists.txt inside it.
5. Click the File Explorer address bar, type powershell and press Enter.
6. Run this command and wait for it to finish:

   cmake -S . -B build-win -G "Visual Studio 17 2022" -A x64

7. Run this command to build the app:

   cmake --build build-win --config Release

8. Open the build-win folder, then the Release folder. Double-click PharmaStock.exe.

After the first build, you can open PharmaStock.exe directly. Leave the two ZIP files inside third_party as they are. CMake extracts them automatically.

HOW TO RUN ON MAC

1. Extract PharmaStock-macOS-arm64.zip on an Apple Silicon Mac.
2. Double-click PharmaStock.app.

To build from source on Mac, install CMake and the Xcode Command Line Tools. Open Terminal in the folder containing CMakeLists.txt and run these commands one at a time:

   cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
   cmake --build build --parallel
   open build/PharmaStock.app

HOW THE PROJECT WORKS

The project uses C++17, Dear ImGui, GLFW, OpenGL and CMake. The GUI displays the six tabs. A shared inventory model handles stock changes, orders and sales, so a sale made in one tab updates the stock shown in the others.

DATA STRUCTURES AND ALGORITHMS

- Dynamic array – Stores medicine records and grows when more space is needed.
- FIFO queue – Processes customer orders in the order they arrive.
- Min-heap – Gives priority to the batch with the earliest expiry date.
- Adjacency list and breadth-first search (BFS) – Store supplier connections and find reachable suppliers.
- Linear search – Finds medicines by scanning the inventory.
- Bubble sort – Sorts a copy of the inventory and counts comparisons and swaps.

SUPPLIER NETWORK

Distributors: Ravi Distribution and Mehran Distribution.
Suppliers: Ali Pharma, Shifa Medical and Margalla Pharma.

