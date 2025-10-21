<!DOCTYPE html>
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Inventaris Lab Komputer</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            box-sizing: border-box;
        }
        .fade-in {
            animation: fadeIn 0.3s ease-in;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .chart-bar {
            transition: all 0.3s ease;
        }
        .chart-bar:hover {
            transform: scaleY(1.05);
        }
    </style>
</head>
<body class="h-full bg-gradient-to-br from-blue-50 to-indigo-100 font-sans">
    <!-- Login Screen -->
    <div id="loginScreen" class="flex items-center justify-center h-full">
        <div class="bg-white rounded-lg shadow-xl p-8 w-full max-w-md mx-4">
            <div class="text-center mb-8">
                <div class="text-4xl mb-4">💻</div>
                <h1 class="text-2xl font-bold text-gray-800 mb-2">Lab Inventory System</h1>
                <p class="text-gray-600">SMK NU 1 ISLAMIYAH KRAMAT</p>
            </div>
            
            <form onsubmit="handleLogin(event)" class="space-y-6">
                <div>
                    <label for="username" class="block text-sm font-medium text-gray-700 mb-2">Username</label>
                    <input type="text" id="username" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Masukkan username">
                </div>
                
                <div>
                    <label for="password" class="block text-sm font-medium text-gray-700 mb-2">Password</label>
                    <input type="password" id="password" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Masukkan password">
                </div>
                
                <div id="loginError" class="hidden bg-red-50 border border-red-200 text-red-700 px-4 py-3 rounded-lg text-sm">
                    Username atau password salah!
                </div>
                
                <button type="submit" class="w-full bg-blue-500 hover:bg-blue-600 text-white font-medium py-3 px-4 rounded-lg transition-colors">
                    🔐 Masuk ke Sistem
                </button>
            </form>
            
            <div class="mt-6 text-center">
                <div class="bg-gray-50 rounded-lg p-4">
                    <p class="text-sm text-gray-600 mb-2">Demo Login:</p>
                    <p class="text-xs text-gray-500">Username: <strong>admin</strong></p>
                    <p class="text-xs text-gray-500">Password: <strong>admin</strong></p>
                </div>
            </div>
            
            <div class="mt-6 text-center text-xs text-gray-500">
                <p>© 2024 Lab Inventory System v2.0.0</p>
                <p>Developed by Ahmad Mashuri, S.Kom</p>
            </div>
        </div>
    </div>

    <!-- Main Application -->
    <div id="mainApp" class="flex h-full hidden">
        <!-- Sidebar -->
        <div class="w-64 bg-white shadow-lg">
            <div class="p-6 border-b border-gray-200">
                <h1 class="text-xl font-bold text-gray-800">💻 Lab Inventory</h1>
                <p class="text-sm text-gray-600 mt-1">Sistem Inventaris Lab</p>
                <button onclick="logout()" class="mt-3 w-full text-left px-3 py-2 text-sm text-red-600 hover:bg-red-50 rounded-md transition-colors flex items-center space-x-2">
                    <span>🚪</span>
                    <span>Logout</span>
                </button>
            </div>
            <nav class="mt-6">
                <button onclick="showPage('dashboard')" class="nav-btn w-full text-left px-6 py-3 text-gray-700 hover:bg-blue-50 hover:text-blue-600 transition-colors flex items-center space-x-3 border-l-4 border-blue-500 bg-blue-50 text-blue-600">
                    <span>📊</span>
                    <span>Dashboard</span>
                </button>
                <button onclick="showPage('inventory')" class="nav-btn w-full text-left px-6 py-3 text-gray-700 hover:bg-blue-50 hover:text-blue-600 transition-colors flex items-center space-x-3 border-l-4 border-transparent">
                    <span>📦</span>
                    <span>Inventaris Barang</span>
                </button>
                <button onclick="showPage('transactions')" class="nav-btn w-full text-left px-6 py-3 text-gray-700 hover:bg-blue-50 hover:text-blue-600 transition-colors flex items-center space-x-3 border-l-4 border-transparent">
                    <span>🔄</span>
                    <span>Keluar Masuk Barang</span>
                </button>
                <button onclick="showPage('stock')" class="nav-btn w-full text-left px-6 py-3 text-gray-700 hover:bg-blue-50 hover:text-blue-600 transition-colors flex items-center space-x-3 border-l-4 border-transparent">
                    <span>📦</span>
                    <span>Stok Barang</span>
                </button>
                <button onclick="showPage('reports')" class="nav-btn w-full text-left px-6 py-3 text-gray-700 hover:bg-blue-50 hover:text-blue-600 transition-colors flex items-center space-x-3 border-l-4 border-transparent">
                    <span>📈</span>
                    <span>Laporan Bulanan</span>
                </button>
                <button onclick="showPage('location-reports')" class="nav-btn w-full text-left px-6 py-3 text-gray-700 hover:bg-blue-50 hover:text-blue-600 transition-colors flex items-center space-x-3 border-l-4 border-transparent">
                    <span>📍</span>
                    <span>Laporan Per Lokasi</span>
                </button>
                <button onclick="showPage('about')" class="nav-btn w-full text-left px-6 py-3 text-gray-700 hover:bg-blue-50 hover:text-blue-600 transition-colors flex items-center space-x-3 border-l-4 border-transparent">
                    <span>ℹ️</span>
                    <span>Tentang Aplikasi</span>
                </button>
            </nav>
        </div>

        <!-- Main Content -->
        <div class="flex-1 overflow-auto">
            <!-- Dashboard Page -->
            <div id="dashboard" class="page p-8">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-800 mb-2">📊 Dashboard</h2>
                    <p class="text-gray-600">Ringkasan inventaris lab komputer</p>
                </div>

                <!-- Stats Cards -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                    <div class="bg-white rounded-lg shadow-md p-6 border-l-4 border-blue-500">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm text-gray-600">Total Barang</p>
                                <p id="total-items" class="text-2xl font-bold text-gray-800">0</p>
                            </div>
                            <div class="text-3xl">💻</div>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow-md p-6 border-l-4 border-green-500">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm text-gray-600">Barang Tersedia</p>
                                <p id="available-items" class="text-2xl font-bold text-gray-800">0</p>
                            </div>
                            <div class="text-3xl">✅</div>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow-md p-6 border-l-4 border-yellow-500">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm text-gray-600">Perlu Perbaikan</p>
                                <p id="repair-items" class="text-2xl font-bold text-gray-800">0</p>
                            </div>
                            <div class="text-3xl">⚠️</div>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow-md p-6 border-l-4 border-red-500">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm text-gray-600">Rusak</p>
                                <p id="broken-items" class="text-2xl font-bold text-gray-800">0</p>
                            </div>
                            <div class="text-3xl">❌</div>
                        </div>
                    </div>
                </div>

                <!-- Charts -->
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <div class="bg-white rounded-lg shadow-md p-6">
                        <h3 class="text-lg font-semibold text-gray-800 mb-4">Kategori Barang</h3>
                        <div id="category-chart" class="space-y-4">
                            <!-- Dynamic category chart will be populated here -->
                        </div>
                    </div>

                    <div class="bg-white rounded-lg shadow-md p-6">
                        <h3 class="text-lg font-semibold text-gray-800 mb-4">Aktivitas Terbaru</h3>
                        <div id="recent-activities" class="space-y-4">
                            <!-- Recent activities will be populated here -->
                        </div>
                    </div>
                </div>
            </div>

            <!-- Inventory Page -->
            <div id="inventory" class="page p-8 hidden">
                <div class="mb-8 flex justify-between items-center">
                    <div>
                        <h2 class="text-3xl font-bold text-gray-800 mb-2">📦 Inventaris Barang</h2>
                        <p class="text-gray-600">Kelola semua barang inventaris lab</p>
                    </div>
                    <button onclick="showAddItemModal()" class="bg-blue-500 hover:bg-blue-600 text-white px-6 py-2 rounded-lg transition-colors">
                        ➕ Tambah Barang
                    </button>
                </div>

                <!-- Search and Filter -->
                <div class="bg-white rounded-lg shadow-md p-6 mb-6">
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div>
                            <label for="search-item" class="block text-sm font-medium text-gray-700 mb-2">Cari Barang</label>
                            <input type="text" id="search-item" placeholder="Nama barang..." class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                        </div>
                        <div>
                            <label for="filter-category" class="block text-sm font-medium text-gray-700 mb-2">Kategori</label>
                            <select id="filter-category" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                                <option value="">Semua Kategori</option>
                                <option value="komputer">Komputer</option>
                                <option value="alat-praktik">Alat Praktik</option>
                                <option value="laptop">Laptop</option>
                                <option value="printer">Printer</option>
                                <option value="jaringan">Jaringan</option>
                                <option value="peripheral">Peripheral</option>
                                <option value="lainnya">Lainnya</option>
                            </select>
                        </div>
                        <div>
                            <label for="filter-status" class="block text-sm font-medium text-gray-700 mb-2">Status</label>
                            <select id="filter-status" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                                <option value="">Semua Status</option>
                                <option value="baik">Baik</option>
                                <option value="perbaikan">Perlu Perbaikan</option>
                                <option value="rusak">Rusak</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- Inventory Table -->
                <div class="bg-white rounded-lg shadow-md overflow-hidden">
                    <table class="w-full">
                        <thead class="bg-gray-50">
                            <tr>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kode</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Nama Barang</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kategori</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kondisi</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tahun</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Lokasi</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="inventory-table" class="bg-white divide-y divide-gray-200">
                            <!-- Dynamic inventory data will be populated here -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Transactions Page -->
            <div id="transactions" class="page p-8 hidden">
                <div class="mb-8 flex justify-between items-center">
                    <div>
                        <h2 class="text-3xl font-bold text-gray-800 mb-2">🔄 Keluar Masuk Barang</h2>
                        <p class="text-gray-600">Catat transaksi barang masuk dan keluar</p>
                    </div>
                    <button onclick="showTransactionModal()" class="bg-green-500 hover:bg-green-600 text-white px-6 py-2 rounded-lg transition-colors">
                        ➕ Tambah Transaksi
                    </button>
                </div>

                <!-- Transaction Stats -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-6">
                    <div class="bg-white rounded-lg shadow-md p-6 border-l-4 border-green-500">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm text-gray-600">Barang Masuk Hari Ini</p>
                                <p id="today-in" class="text-2xl font-bold text-gray-800">0</p>
                            </div>
                            <div class="text-3xl">📥</div>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow-md p-6 border-l-4 border-red-500">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm text-gray-600">Barang Keluar Hari Ini</p>
                                <p id="today-out" class="text-2xl font-bold text-gray-800">0</p>
                            </div>
                            <div class="text-3xl">📤</div>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow-md p-6 border-l-4 border-blue-500">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm text-gray-600">Total Transaksi Bulan Ini</p>
                                <p id="month-transactions" class="text-2xl font-bold text-gray-800">0</p>
                            </div>
                            <div class="text-3xl">📊</div>
                        </div>
                    </div>
                </div>

                <!-- Transaction History -->
                <div class="bg-white rounded-lg shadow-md overflow-hidden">
                    <div class="px-6 py-4 border-b border-gray-200">
                        <h3 class="text-lg font-semibold text-gray-800">Riwayat Transaksi</h3>
                    </div>
                    <table class="w-full">
                        <thead class="bg-gray-50">
                            <tr>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tanggal</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Jenis</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Barang</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Jumlah</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Keterangan</th>
                            </tr>
                        </thead>
                        <tbody id="transaction-table" class="bg-white divide-y divide-gray-200">
                            <!-- Dynamic transaction data will be populated here -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Stock Page -->
            <div id="stock" class="page p-8 hidden">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-800 mb-2">📦 Stok Barang</h2>
                    <p class="text-gray-600">Monitor stok dan peringatan barang menipis</p>
                </div>

                <!-- Stock Alerts -->
                <div id="stock-alerts" class="mb-6">
                    <!-- Dynamic stock alerts will be populated here -->
                </div>

                <!-- Stock Overview -->
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <div class="bg-white rounded-lg shadow-md p-6">
                        <h3 class="text-lg font-semibold text-gray-800 mb-4">Stok per Kategori</h3>
                        <div id="stock-by-category" class="space-y-4">
                            <!-- Dynamic stock by category will be populated here -->
                        </div>
                    </div>

                    <div class="bg-white rounded-lg shadow-md p-6">
                        <h3 class="text-lg font-semibold text-gray-800 mb-4">Barang Perlu Restok</h3>
                        <div id="restock-needed" class="space-y-3">
                            <!-- Dynamic restock items will be populated here -->
                        </div>
                    </div>
                </div>
            </div>

            <!-- Reports Page -->
            <div id="reports" class="page p-8 hidden">
                <div class="mb-8">
                    <div class="bg-white rounded-lg shadow-md p-6 mb-6">
                        <div class="text-center">
                            <h1 class="text-2xl font-bold text-gray-800 mb-1">SMK NU 1 ISLAMIYAH KRAMAT</h1>
                            <p class="text-gray-600 mb-4">Sistem Inventaris Lab Komputer</p>
                        </div>
                    </div>
                    <h2 class="text-3xl font-bold text-gray-800 mb-2">📈 Laporan Bulanan</h2>
                    <p class="text-gray-600">Laporan dan analisis inventaris bulanan</p>
                </div>

                <!-- Report Controls -->
                <div class="bg-white rounded-lg shadow-md p-6 mb-6">
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div>
                            <label for="report-month" class="block text-sm font-medium text-gray-700 mb-2">Bulan</label>
                            <select id="report-month" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                                <option value="2024-01" selected>Januari 2024</option>
                                <option value="2023-12">Desember 2023</option>
                                <option value="2023-11">November 2023</option>
                            </select>
                        </div>
                        <div>
                            <label for="report-type" class="block text-sm font-medium text-gray-700 mb-2">Jenis Laporan</label>
                            <select id="report-type" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                                <option value="summary">Ringkasan</option>
                                <option value="detailed">Detail</option>
                                <option value="category">Per Kategori</option>
                            </select>
                        </div>
                        <div class="flex items-end space-x-2">
                            <button onclick="generateReport()" class="flex-1 bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-md transition-colors">
                                📊 Generate Laporan
                            </button>
                            <button onclick="printReport()" class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-md transition-colors">
                                🖨️ Cetak
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Report Summary -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-6">
                    <div class="bg-white rounded-lg shadow-md p-6 text-center">
                        <div class="text-3xl mb-2">📥</div>
                        <p id="report-in" class="text-2xl font-bold text-gray-800">0</p>
                        <p class="text-sm text-gray-600">Barang Masuk</p>
                    </div>
                    <div class="bg-white rounded-lg shadow-md p-6 text-center">
                        <div class="text-3xl mb-2">📤</div>
                        <p id="report-out" class="text-2xl font-bold text-gray-800">0</p>
                        <p class="text-sm text-gray-600">Barang Keluar</p>
                    </div>
                    <div class="bg-white rounded-lg shadow-md p-6 text-center">
                        <div class="text-3xl mb-2">🔧</div>
                        <p id="report-repair" class="text-2xl font-bold text-gray-800">0</p>
                        <p class="text-sm text-gray-600">Perbaikan</p>
                    </div>
                    <div class="bg-white rounded-lg shadow-md p-6 text-center">
                        <div class="text-3xl mb-2">💰</div>
                        <p id="report-value" class="text-2xl font-bold text-gray-800">Rp 0</p>
                        <p class="text-sm text-gray-600">Nilai Inventaris</p>
                    </div>
                </div>

                <!-- Detailed Report -->
                <div class="bg-white rounded-lg shadow-md p-6">
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="text-lg font-semibold text-gray-800">Laporan Detail</h3>
                        <button onclick="exportPDF()" class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-md transition-colors text-sm">
                            📄 Export PDF
                        </button>
                    </div>
                    
                    <div id="detailed-report" class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                        <!-- Dynamic detailed report will be populated here -->
                    </div>
                </div>
            </div>

            <!-- Location Reports Page -->
            <div id="location-reports" class="page p-8 hidden">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-800 mb-2">📍 Laporan Per Lokasi</h2>
                    <p class="text-gray-600">Analisis inventaris berdasarkan lokasi penempatan</p>
                </div>

                <!-- Location Filter -->
                <div class="bg-white rounded-lg shadow-md p-6 mb-6">
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div>
                            <label for="location-filter" class="block text-sm font-medium text-gray-700 mb-2">Pilih Lokasi</label>
                            <select id="location-filter" onchange="filterByLocation()" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                                <option value="">Semua Lokasi</option>
                            </select>
                        </div>
                        <div>
                            <label for="location-period" class="block text-sm font-medium text-gray-700 mb-2">Periode</label>
                            <select id="location-period" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                                <option value="2024-01">Januari 2024</option>
                                <option value="2023-12">Desember 2023</option>
                                <option value="2023-11">November 2023</option>
                            </select>
                        </div>
                        <div class="flex items-end space-x-2">
                            <button onclick="generateLocationReport()" class="flex-1 bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-md transition-colors">
                                📊 Generate Laporan
                            </button>
                            <button onclick="printLocationReport()" class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-md transition-colors">
                                🖨️ Cetak
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Location Overview Cards -->
                <div id="location-cards" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-6">
                    <!-- Dynamic location cards will be populated here -->
                </div>

                <!-- Detailed Location Report -->
                <div class="bg-white rounded-lg shadow-md overflow-hidden">
                    <div class="px-6 py-4 border-b border-gray-200">
                        <h3 class="text-lg font-semibold text-gray-800">Detail Barang Per Lokasi</h3>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50">
                                <tr>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Lokasi</th>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kode Barang</th>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Nama Barang</th>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kategori</th>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kondisi</th>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tahun</th>
                                </tr>
                            </thead>
                            <tbody id="location-report-table" class="bg-white divide-y divide-gray-200">
                                <!-- Dynamic location report data will be populated here -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- About Page -->
            <div id="about" class="page p-8 hidden">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-800 mb-2">ℹ️ Tentang Aplikasi</h2>
                    <p class="text-gray-600">Informasi sistem inventaris lab komputer</p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <div class="bg-white rounded-lg shadow-md p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">📋 Informasi Sistem</h3>
                        <div class="space-y-3">
                            <div class="flex justify-between">
                                <span class="text-gray-600">Nama Aplikasi:</span>
                                <span class="font-medium">Lab Inventory System</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-gray-600">Versi:</span>
                                <span class="font-medium">2.0.0</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-gray-600">Tanggal Rilis:</span>
                                <span class="font-medium">15 Januari 2024</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-gray-600">Developer:</span>
                                <span class="font-medium">Ahmad Mashuri, S.Kom</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-gray-600">Database:</span>
                                <span class="font-medium">LocalStorage</span>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white rounded-lg shadow-md p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">🎯 Fitur Utama</h3>
                        <ul class="space-y-2">
                            <li class="flex items-center space-x-2">
                                <span class="text-green-500">✅</span>
                                <span class="text-gray-700">Database terintegrasi</span>
                            </li>
                            <li class="flex items-center space-x-2">
                                <span class="text-green-500">✅</span>
                                <span class="text-gray-700">Dashboard monitoring real-time</span>
                            </li>
                            <li class="flex items-center space-x-2">
                                <span class="text-green-500">✅</span>
                                <span class="text-gray-700">Manajemen inventaris lengkap</span>
                            </li>
                            <li class="flex items-center space-x-2">
                                <span class="text-green-500">✅</span>
                                <span class="text-gray-700">Tracking barang masuk/keluar</span>
                            </li>
                            <li class="flex items-center space-x-2">
                                <span class="text-green-500">✅</span>
                                <span class="text-gray-700">Monitor stok otomatis</span>
                            </li>
                            <li class="flex items-center space-x-2">
                                <span class="text-green-500">✅</span>
                                <span class="text-gray-700">Laporan per lokasi</span>
                            </li>
                        </ul>
                    </div>

                    <div class="bg-white rounded-lg shadow-md p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">📞 Kontak Support</h3>
                        <div class="space-y-3">
                            <div class="flex items-center space-x-3">
                                <span class="text-blue-500">📧</span>
                                <span class="text-gray-700">support@labinventory.com</span>
                            </div>
                            <div class="flex items-center space-x-3">
                                <span class="text-green-500">📱</span>
                                <span class="text-gray-700">081902413975</span>
                            </div>
                            <div class="flex items-center space-x-3">
                                <span class="text-purple-500">🌐</span>
                                <span class="text-gray-700">www.labinventory.com</span>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white rounded-lg shadow-md p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">🗄️ Manajemen Database</h3>
                        <div class="space-y-2">
                            <button onclick="exportDatabase()" class="w-full text-left p-3 bg-blue-50 hover:bg-blue-100 rounded-lg transition-colors">
                                📤 Export Database
                            </button>
                            <button onclick="importDatabase()" class="w-full text-left p-3 bg-green-50 hover:bg-green-100 rounded-lg transition-colors">
                                📥 Import Database
                            </button>
                            <button onclick="clearDatabase()" class="w-full text-left p-3 bg-red-50 hover:bg-red-100 rounded-lg transition-colors">
                                🗑️ Reset Database
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Item Modal -->
    <div id="addItemModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-lg p-6 w-full max-w-md mx-4">
            <h3 class="text-lg font-semibold text-gray-800 mb-4">➕ Tambah Barang Baru</h3>
            <form onsubmit="addNewItem(event)">
                <div class="space-y-4">
                    <div>
                        <label for="item-code" class="block text-sm font-medium text-gray-700 mb-1">Kode Barang</label>
                        <input type="text" id="item-code" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label for="item-name" class="block text-sm font-medium text-gray-700 mb-1">Nama Barang</label>
                        <input type="text" id="item-name" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label for="item-category" class="block text-sm font-medium text-gray-700 mb-1">Kategori</label>
                        <select id="item-category" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="">Pilih Kategori</option>
                            <option value="komputer">Komputer</option>
                            <option value="alat-praktik">Alat Praktik</option>
                            <option value="laptop">Laptop</option>
                            <option value="printer">Printer</option>
                            <option value="jaringan">Jaringan</option>
                            <option value="peripheral">Peripheral</option>
                            <option value="lainnya">Lainnya</option>
                        </select>
                    </div>
                    <div>
                        <label for="item-condition" class="block text-sm font-medium text-gray-700 mb-1">Kondisi Barang (%)</label>
                        <input type="number" id="item-condition" required min="0" max="100" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label for="item-year" class="block text-sm font-medium text-gray-700 mb-1">Tahun Barang</label>
                        <input type="number" id="item-year" required min="2000" max="2030" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label for="item-location" class="block text-sm font-medium text-gray-700 mb-1">Lokasi</label>
                        <input type="text" id="item-location" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label for="item-quantity" class="block text-sm font-medium text-gray-700 mb-1">Jumlah</label>
                        <input type="number" id="item-quantity" required min="1" value="1" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>
                <div class="flex justify-end space-x-3 mt-6">
                    <button type="button" onclick="hideAddItemModal()" class="px-4 py-2 text-gray-600 hover:text-gray-800 transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="px-4 py-2 bg-blue-500 hover:bg-blue-600 text-white rounded-md transition-colors">
                        Simpan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Transaction Modal -->
    <div id="transactionModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-lg p-6 w-full max-w-md mx-4">
            <h3 class="text-lg font-semibold text-gray-800 mb-4">➕ Tambah Transaksi</h3>
            <form onsubmit="addNewTransaction(event)">
                <div class="space-y-4">
                    <div>
                        <label for="trans-date" class="block text-sm font-medium text-gray-700 mb-1">Tanggal Transaksi</label>
                        <input type="date" id="trans-date" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label for="trans-type" class="block text-sm font-medium text-gray-700 mb-1">Jenis Transaksi</label>
                        <select id="trans-type" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="">Pilih Jenis</option>
                            <option value="masuk">Barang Masuk</option>
                            <option value="keluar">Barang Keluar</option>
                        </select>
                    </div>
                    <div>
                        <label for="trans-item" class="block text-sm font-medium text-gray-700 mb-1">Pilih Barang</label>
                        <select id="trans-item" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="">Pilih Barang</option>
                        </select>
                    </div>
                    <div>
                        <label for="trans-quantity" class="block text-sm font-medium text-gray-700 mb-1">Jumlah</label>
                        <input type="number" id="trans-quantity" required min="1" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label for="trans-note" class="block text-sm font-medium text-gray-700 mb-1">Keterangan</label>
                        <textarea id="trans-note" rows="3" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
                    </div>
                </div>
                <div class="flex justify-end space-x-3 mt-6">
                    <button type="button" onclick="hideTransactionModal()" class="px-4 py-2 text-gray-600 hover:text-gray-800 transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="px-4 py-2 bg-green-500 hover:bg-green-600 text-white rounded-md transition-colors">
                        Simpan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // Database Management System
        class InventoryDatabase {
            constructor() {
                this.items = this.loadData('inventory_items') || [];
                this.transactions = this.loadData('inventory_transactions') || [];
                this.categories = ['komputer', 'alat-praktik', 'laptop', 'printer', 'jaringan', 'peripheral', 'lainnya'];
                this.locations = new Set();
                this.initializeData();
            }

            loadData(key) {
                try {
                    const data = localStorage.getItem(key);
                    return data ? JSON.parse(data) : null;
                } catch (error) {
                    console.error('Error loading data:', error);
                    return null;
                }
            }

            saveData(key, data) {
                try {
                    localStorage.setItem(key, JSON.stringify(data));
                    return true;
                } catch (error) {
                    console.error('Error saving data:', error);
                    return false;
                }
            }

            initializeData() {
                if (this.items.length === 0) {
                    // Initialize with sample data
                    this.items = [
                        {
                            id: 'PC001',
                            code: 'PC001',
                            name: 'Dell OptiPlex 3070',
                            category: 'komputer',
                            condition: 95,
                            year: 2023,
                            location: 'Lab A - Meja 1',
                            quantity: 1,
                            createdAt: new Date().toISOString()
                        },
                        {
                            id: 'LAP001',
                            code: 'LAP001',
                            name: 'Lenovo ThinkPad E14',
                            category: 'laptop',
                            condition: 88,
                            year: 2022,
                            location: 'Lab B - Meja 5',
                            quantity: 1,
                            createdAt: new Date().toISOString()
                        },
                        {
                            id: 'PRT001',
                            code: 'PRT001',
                            name: 'HP LaserJet Pro M404n',
                            category: 'printer',
                            condition: 65,
                            year: 2021,
                            location: 'Ruang Guru',
                            quantity: 1,
                            createdAt: new Date().toISOString()
                        }
                    ];
                    this.saveItems();
                }

                if (this.transactions.length === 0) {
                    // Initialize with sample transactions
                    this.transactions = [
                        {
                            id: 'TRX001',
                            date: new Date().toISOString(),
                            type: 'masuk',
                            itemId: 'PC001',
                            itemName: 'Dell OptiPlex 3070',
                            quantity: 5,
                            note: 'Pembelian baru',
                            createdAt: new Date().toISOString()
                        }
                    ];
                    this.saveTransactions();
                }

                this.updateLocations();
            }

            updateLocations() {
                this.locations.clear();
                this.items.forEach(item => {
                    if (item.location) {
                        this.locations.add(item.location.split(' - ')[0]); // Extract main location
                    }
                });
            }

            // Item management
            addItem(itemData) {
                const item = {
                    id: itemData.code,
                    code: itemData.code,
                    name: itemData.name,
                    category: itemData.category,
                    condition: parseInt(itemData.condition),
                    year: parseInt(itemData.year),
                    location: itemData.location,
                    quantity: parseInt(itemData.quantity),
                    createdAt: new Date().toISOString()
                };

                this.items.push(item);
                this.saveItems();
                this.updateLocations();
                
                // Add transaction for new item
                this.addTransaction({
                    type: 'masuk',
                    itemId: item.id,
                    itemName: item.name,
                    quantity: item.quantity,
                    note: 'Barang baru ditambahkan'
                });

                return item;
            }

            updateItem(id, updates) {
                const index = this.items.findIndex(item => item.id === id);
                if (index !== -1) {
                    this.items[index] = { ...this.items[index], ...updates };
                    this.saveItems();
                    this.updateLocations();
                    return this.items[index];
                }
                return null;
            }

            deleteItem(id) {
                const index = this.items.findIndex(item => item.id === id);
                if (index !== -1) {
                    const item = this.items[index];
                    this.items.splice(index, 1);
                    this.saveItems();
                    this.updateLocations();
                    
                    // Add transaction for deleted item
                    this.addTransaction({
                        type: 'keluar',
                        itemId: item.id,
                        itemName: item.name,
                        quantity: item.quantity,
                        note: 'Barang dihapus dari inventaris'
                    });
                    
                    return item;
                }
                return null;
            }

            getItems(filters = {}) {
                let filteredItems = [...this.items];

                if (filters.search) {
                    const search = filters.search.toLowerCase();
                    filteredItems = filteredItems.filter(item => 
                        item.name.toLowerCase().includes(search) ||
                        item.code.toLowerCase().includes(search)
                    );
                }

                if (filters.category) {
                    filteredItems = filteredItems.filter(item => item.category === filters.category);
                }

                if (filters.status) {
                    filteredItems = filteredItems.filter(item => {
                        const status = this.getItemStatus(item.condition);
                        return status === filters.status;
                    });
                }

                if (filters.location) {
                    filteredItems = filteredItems.filter(item => 
                        item.location.toLowerCase().includes(filters.location.toLowerCase())
                    );
                }

                return filteredItems;
            }

            getItemStatus(condition) {
                if (condition >= 80) return 'baik';
                if (condition >= 50) return 'perbaikan';
                return 'rusak';
            }

            // Transaction management
            addTransaction(transactionData) {
                const transaction = {
                    id: 'TRX' + Date.now(),
                    date: transactionData.date || new Date().toISOString(),
                    type: transactionData.type,
                    itemId: transactionData.itemId,
                    itemName: transactionData.itemName,
                    quantity: parseInt(transactionData.quantity),
                    note: transactionData.note || '',
                    createdAt: new Date().toISOString()
                };

                this.transactions.push(transaction);
                this.saveTransactions();
                return transaction;
            }

            getTransactions(filters = {}) {
                let filteredTransactions = [...this.transactions];

                if (filters.type) {
                    filteredTransactions = filteredTransactions.filter(t => t.type === filters.type);
                }

                if (filters.dateFrom) {
                    filteredTransactions = filteredTransactions.filter(t => 
                        new Date(t.date) >= new Date(filters.dateFrom)
                    );
                }

                if (filters.dateTo) {
                    filteredTransactions = filteredTransactions.filter(t => 
                        new Date(t.date) <= new Date(filters.dateTo)
                    );
                }

                return filteredTransactions.sort((a, b) => new Date(b.date) - new Date(a.date));
            }

            // Statistics and analytics
            getStats() {
                const total = this.items.length;
                const available = this.items.filter(item => this.getItemStatus(item.condition) === 'baik').length;
                const repair = this.items.filter(item => this.getItemStatus(item.condition) === 'perbaikan').length;
                const broken = this.items.filter(item => this.getItemStatus(item.condition) === 'rusak').length;

                const today = new Date().toDateString();
                const todayTransactions = this.transactions.filter(t => 
                    new Date(t.date).toDateString() === today
                );
                const todayIn = todayTransactions.filter(t => t.type === 'masuk').length;
                const todayOut = todayTransactions.filter(t => t.type === 'keluar').length;

                const thisMonth = new Date().getMonth();
                const thisYear = new Date().getFullYear();
                const monthTransactions = this.transactions.filter(t => {
                    const date = new Date(t.date);
                    return date.getMonth() === thisMonth && date.getFullYear() === thisYear;
                }).length;

                const totalValue = this.items.reduce((sum, item) => sum + (item.quantity * 1000000), 0);

                return {
                    total,
                    available,
                    repair,
                    broken,
                    todayIn,
                    todayOut,
                    monthTransactions,
                    totalValue
                };
            }

            getCategoryStats() {
                const categoryStats = {};
                this.categories.forEach(category => {
                    categoryStats[category] = this.items.filter(item => item.category === category).length;
                });
                return categoryStats;
            }

            getLocationStats() {
                const locationStats = {};
                Array.from(this.locations).forEach(location => {
                    const locationItems = this.items.filter(item => 
                        item.location.toLowerCase().includes(location.toLowerCase())
                    );
                    
                    const total = locationItems.length;
                    const good = locationItems.filter(item => this.getItemStatus(item.condition) === 'baik').length;
                    const repair = locationItems.filter(item => this.getItemStatus(item.condition) === 'perbaikan').length;
                    const broken = locationItems.filter(item => this.getItemStatus(item.condition) === 'rusak').length;
                    const health = total > 0 ? Math.round((good / total) * 100) : 0;

                    locationStats[location] = { total, good, repair, broken, health };
                });
                return locationStats;
            }

            // Data persistence
            saveItems() {
                return this.saveData('inventory_items', this.items);
            }

            saveTransactions() {
                return this.saveData('inventory_transactions', this.transactions);
            }

            // Database management
            exportDatabase() {
                return {
                    items: this.items,
                    transactions: this.transactions,
                    exportDate: new Date().toISOString(),
                    version: '2.0.0'
                };
            }

            importDatabase(data) {
                try {
                    if (data.items && Array.isArray(data.items)) {
                        this.items = data.items;
                        this.saveItems();
                    }
                    if (data.transactions && Array.isArray(data.transactions)) {
                        this.transactions = data.transactions;
                        this.saveTransactions();
                    }
                    this.updateLocations();
                    return true;
                } catch (error) {
                    console.error('Error importing database:', error);
                    return false;
                }
            }

            clearDatabase() {
                this.items = [];
                this.transactions = [];
                this.locations.clear();
                localStorage.removeItem('inventory_items');
                localStorage.removeItem('inventory_transactions');
                return true;
            }
        }

        // Initialize database
        const db = new InventoryDatabase();

        // UI Management
        class InventoryUI {
            constructor(database) {
                this.db = database;
                this.currentPage = 'dashboard';
                this.init();
            }

            init() {
                this.updateDashboard();
                this.updateInventoryTable();
                this.updateTransactionTable();
                this.updateStockPage();
                this.updateLocationReports();
                this.populateTransactionItemSelect();
                this.populateLocationFilter();
                this.setupEventListeners();
            }

            setupEventListeners() {
                // Search and filter
                document.getElementById('search-item')?.addEventListener('input', (e) => {
                    this.filterInventoryTable();
                });

                document.getElementById('filter-category')?.addEventListener('change', (e) => {
                    this.filterInventoryTable();
                });

                document.getElementById('filter-status')?.addEventListener('change', (e) => {
                    this.filterInventoryTable();
                });
            }

            updateDashboard() {
                const stats = this.db.getStats();
                
                document.getElementById('total-items').textContent = stats.total;
                document.getElementById('available-items').textContent = stats.available;
                document.getElementById('repair-items').textContent = stats.repair;
                document.getElementById('broken-items').textContent = stats.broken;

                // Update category chart
                this.updateCategoryChart();
                
                // Update recent activities
                this.updateRecentActivities();
            }

            updateCategoryChart() {
                const categoryStats = this.db.getCategoryStats();
                const chartContainer = document.getElementById('category-chart');
                
                const categoryNames = {
                    'komputer': 'Komputer',
                    'alat-praktik': 'Alat Praktik',
                    'laptop': 'Laptop',
                    'printer': 'Printer',
                    'jaringan': 'Jaringan',
                    'peripheral': 'Peripheral',
                    'lainnya': 'Lainnya'
                };

                const colors = ['blue', 'green', 'yellow', 'purple', 'indigo', 'pink', 'gray'];
                
                chartContainer.innerHTML = '';
                
                Object.entries(categoryStats).forEach(([category, count], index) => {
                    if (count > 0) {
                        const percentage = Math.max((count / Math.max(...Object.values(categoryStats))) * 100, 10);
                        const color = colors[index % colors.length];
                        
                        const chartItem = document.createElement('div');
                        chartItem.className = 'flex items-center justify-between';
                        chartItem.innerHTML = `
                            <span class="text-gray-600">${categoryNames[category]}</span>
                            <div class="flex items-center space-x-2">
                                <div class="w-32 bg-gray-200 rounded-full h-2">
                                    <div class="bg-${color}-500 h-2 rounded-full chart-bar" style="width: ${percentage}%"></div>
                                </div>
                                <span class="text-sm text-gray-600">${count}</span>
                            </div>
                        `;
                        chartContainer.appendChild(chartItem);
                    }
                });
            }

            updateRecentActivities() {
                const recentTransactions = this.db.getTransactions().slice(0, 3);
                const activitiesContainer = document.getElementById('recent-activities');
                
                activitiesContainer.innerHTML = '';
                
                recentTransactions.forEach(transaction => {
                    const timeAgo = this.getTimeAgo(new Date(transaction.date));
                    const icon = transaction.type === 'masuk' ? '📥' : '📤';
                    const bgColor = transaction.type === 'masuk' ? 'bg-blue-50' : 'bg-green-50';
                    const textColor = transaction.type === 'masuk' ? 'text-blue-500' : 'text-green-500';
                    
                    const activityItem = document.createElement('div');
                    activityItem.className = `flex items-start space-x-3 p-3 ${bgColor} rounded-lg`;
                    activityItem.innerHTML = `
                        <div class="${textColor}">${icon}</div>
                        <div>
                            <p class="text-sm font-medium text-gray-800">${transaction.type === 'masuk' ? 'Barang Masuk' : 'Barang Keluar'}</p>
                            <p class="text-xs text-gray-600">${transaction.itemName} (${transaction.quantity} unit) - ${timeAgo}</p>
                        </div>
                    `;
                    activitiesContainer.appendChild(activityItem);
                });
            }

            updateInventoryTable() {
                const tableBody = document.getElementById('inventory-table');
                const items = this.db.getItems();
                
                tableBody.innerHTML = '';
                
                items.forEach(item => {
                    const status = this.db.getItemStatus(item.condition);
                    const statusConfig = this.getStatusConfig(status);
                    
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.code}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.name}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${this.getCategoryName(item.category)}</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="px-2 py-1 text-xs font-semibold rounded-full ${statusConfig.class}">${statusConfig.text}</span>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${item.condition}%</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${item.year}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${item.location}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                            <button onclick="editItem('${item.id}')" class="text-blue-600 hover:text-blue-900 mr-3">✏️ Edit</button>
                            <button onclick="deleteItem('${item.id}')" class="text-red-600 hover:text-red-900">🗑️ Hapus</button>
                        </td>
                    `;
                    tableBody.appendChild(row);
                });
            }

            filterInventoryTable() {
                const search = document.getElementById('search-item').value;
                const category = document.getElementById('filter-category').value;
                const status = document.getElementById('filter-status').value;
                
                const filters = {};
                if (search) filters.search = search;
                if (category) filters.category = category;
                if (status) filters.status = status;
                
                const filteredItems = this.db.getItems(filters);
                const tableBody = document.getElementById('inventory-table');
                
                tableBody.innerHTML = '';
                
                filteredItems.forEach(item => {
                    const itemStatus = this.db.getItemStatus(item.condition);
                    const statusConfig = this.getStatusConfig(itemStatus);
                    
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.code}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.name}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${this.getCategoryName(item.category)}</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="px-2 py-1 text-xs font-semibold rounded-full ${statusConfig.class}">${statusConfig.text}</span>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${item.condition}%</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${item.year}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${item.location}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                            <button onclick="editItem('${item.id}')" class="text-blue-600 hover:text-blue-900 mr-3">✏️ Edit</button>
                            <button onclick="deleteItem('${item.id}')" class="text-red-600 hover:text-red-900">🗑️ Hapus</button>
                        </td>
                    `;
                    tableBody.appendChild(row);
                });
            }

            updateTransactionTable() {
                const stats = this.db.getStats();
                document.getElementById('today-in').textContent = stats.todayIn;
                document.getElementById('today-out').textContent = stats.todayOut;
                document.getElementById('month-transactions').textContent = stats.monthTransactions;

                const tableBody = document.getElementById('transaction-table');
                const transactions = this.db.getTransactions().slice(0, 10); // Show last 10 transactions
                
                tableBody.innerHTML = '';
                
                transactions.forEach(transaction => {
                    const date = new Date(transaction.date);
                    const dateStr = date.toLocaleDateString('id-ID') + ' ' + date.toLocaleTimeString('id-ID', {hour: '2-digit', minute: '2-digit'});
                    const typeLabel = transaction.type === 'masuk' ? '📥 Masuk' : '📤 Keluar';
                    const typeClass = transaction.type === 'masuk' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800';
                    
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${dateStr}</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="px-2 py-1 text-xs font-semibold rounded-full ${typeClass}">${typeLabel}</span>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${transaction.itemName}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${transaction.quantity}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${transaction.note || '-'}</td>
                    `;
                    tableBody.appendChild(row);
                });
            }

            updateStockPage() {
                const categoryStats = this.db.getCategoryStats();
                const lowStockItems = this.db.getItems().filter(item => item.quantity < 5);
                
                // Update stock alerts
                const alertsContainer = document.getElementById('stock-alerts');
                if (lowStockItems.length > 0) {
                    alertsContainer.innerHTML = `
                        <div class="bg-yellow-50 border-l-4 border-yellow-400 p-4">
                            <div class="flex">
                                <div class="text-yellow-400 text-xl mr-3">⚠️</div>
                                <div>
                                    <h3 class="text-sm font-medium text-yellow-800">Peringatan Stok Menipis</h3>
                                    <p class="text-sm text-yellow-700 mt-1">${lowStockItems.length} item memiliki stok di bawah batas minimum</p>
                                </div>
                            </div>
                        </div>
                    `;
                } else {
                    alertsContainer.innerHTML = '';
                }

                // Update stock by category
                const stockContainer = document.getElementById('stock-by-category');
                stockContainer.innerHTML = '';
                
                const categoryNames = {
                    'komputer': { name: 'Komputer', icon: '💻', color: 'blue' },
                    'laptop': { name: 'Laptop', icon: '💻', color: 'green' },
                    'alat-praktik': { name: 'Alat Praktik', icon: '🔧', color: 'purple' },
                    'printer': { name: 'Printer', icon: '🖨️', color: 'indigo' },
                    'jaringan': { name: 'Jaringan', icon: '🌐', color: 'yellow' },
                    'peripheral': { name: 'Peripheral', icon: '⌨️', color: 'pink' }
                };

                Object.entries(categoryStats).forEach(([category, count]) => {
                    if (count > 0) {
                        const config = categoryNames[category] || { name: category, icon: '📦', color: 'gray' };
                        const status = count < 10 ? 'Menipis' : count < 5 ? 'Kritis' : 'Normal';
                        const statusColor = count < 5 ? 'red' : count < 10 ? 'yellow' : 'green';
                        
                        const stockItem = document.createElement('div');
                        stockItem.className = `flex justify-between items-center p-3 bg-${config.color}-50 rounded-lg`;
                        stockItem.innerHTML = `
                            <div class="flex items-center space-x-3">
                                <span class="text-2xl">${config.icon}</span>
                                <div>
                                    <p class="font-medium text-gray-800">${config.name}</p>
                                    <p class="text-sm text-gray-600">${count} unit tersedia</p>
                                </div>
                            </div>
                            <span class="px-3 py-1 bg-${statusColor}-100 text-${statusColor}-800 text-sm font-medium rounded-full">${status}</span>
                        `;
                        stockContainer.appendChild(stockItem);
                    }
                });

                // Update restock needed
                const restockContainer = document.getElementById('restock-needed');
                restockContainer.innerHTML = '';
                
                lowStockItems.forEach(item => {
                    const borderColor = item.quantity < 3 ? 'red' : 'yellow';
                    const textColor = item.quantity < 3 ? 'red' : 'yellow';
                    
                    const restockItem = document.createElement('div');
                    restockItem.className = `flex items-center justify-between p-3 border border-${borderColor}-200 rounded-lg`;
                    restockItem.innerHTML = `
                        <div>
                            <p class="font-medium text-gray-800">${item.name}</p>
                            <p class="text-sm text-${textColor}-600">Stok: ${item.quantity} unit (Min: 5)</p>
                        </div>
                        <button class="px-3 py-1 bg-blue-500 text-white text-sm rounded hover:bg-blue-600 transition-colors">
                            Pesan
                        </button>
                    `;
                    restockContainer.appendChild(restockItem);
                });
            }

            updateLocationReports() {
                const locationStats = this.db.getLocationStats();
                
                // Update location filter
                this.populateLocationFilter();
                
                // Update location cards
                const cardsContainer = document.getElementById('location-cards');
                cardsContainer.innerHTML = '';
                
                const locationIcons = {
                    'Lab A': '💻',
                    'Lab B': '💻',
                    'Lab Elektronika': '🔧',
                    'Ruang Guru': '🖨️',
                    'Perpustakaan': '📚',
                    'Ruang Server': '🌐'
                };

                const locationColors = {
                    'Lab A': 'blue',
                    'Lab B': 'green',
                    'Lab Elektronika': 'purple',
                    'Ruang Guru': 'yellow',
                    'Perpustakaan': 'indigo',
                    'Ruang Server': 'red'
                };

                Object.entries(locationStats).forEach(([location, stats]) => {
                    const icon = locationIcons[location] || '📦';
                    const color = locationColors[location] || 'gray';
                    const healthColor = stats.health >= 90 ? 'green' : stats.health >= 80 ? 'yellow' : 'red';
                    
                    const card = document.createElement('div');
                    card.className = `bg-white rounded-lg shadow-md p-6 border-l-4 border-${color}-500`;
                    card.innerHTML = `
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-lg font-semibold text-gray-800">${location}</h3>
                            <span class="text-2xl">${icon}</span>
                        </div>
                        <div class="space-y-2">
                            <div class="flex justify-between text-sm">
                                <span class="text-gray-600">Total Barang:</span>
                                <span class="font-medium">${stats.total} unit</span>
                            </div>
                            <div class="flex justify-between text-sm">
                                <span class="text-gray-600">Kondisi Baik:</span>
                                <span class="font-medium text-green-600">${stats.good} unit</span>
                            </div>
                            <div class="flex justify-between text-sm">
                                <span class="text-gray-600">Perlu Perbaikan:</span>
                                <span class="font-medium text-yellow-600">${stats.repair} unit</span>
                            </div>
                            <div class="flex justify-between text-sm">
                                <span class="text-gray-600">Rusak:</span>
                                <span class="font-medium text-red-600">${stats.broken} unit</span>
                            </div>
                        </div>
                        <div class="mt-4 pt-4 border-t border-gray-200">
                            <div class="flex justify-between text-sm">
                                <span class="text-gray-600">Tingkat Kesehatan:</span>
                                <span class="font-medium text-${healthColor}-600">${stats.health}%</span>
                            </div>
                        </div>
                    `;
                    cardsContainer.appendChild(card);
                });

                // Update location report table
                this.updateLocationReportTable();
            }

            updateLocationReportTable() {
                const tableBody = document.getElementById('location-report-table');
                const items = this.db.getItems();
                
                tableBody.innerHTML = '';
                
                items.forEach(item => {
                    const status = this.db.getItemStatus(item.condition);
                    const statusConfig = this.getStatusConfig(status);
                    
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${item.location}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.code}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.name}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${this.getCategoryName(item.category)}</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="px-2 py-1 text-xs font-semibold rounded-full ${statusConfig.class}">${statusConfig.text}</span>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${item.condition}%</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-600">${item.year}</td>
                    `;
                    tableBody.appendChild(row);
                });
            }

            populateTransactionItemSelect() {
                const select = document.getElementById('trans-item');
                const items = this.db.getItems();
                
                select.innerHTML = '<option value="">Pilih Barang</option>';
                
                items.forEach(item => {
                    const option = document.createElement('option');
                    option.value = item.id;
                    option.textContent = `${item.code} - ${item.name}`;
                    select.appendChild(option);
                });
            }

            populateLocationFilter() {
                const select = document.getElementById('location-filter');
                const locations = Array.from(this.db.locations);
                
                select.innerHTML = '<option value="">Semua Lokasi</option>';
                
                locations.forEach(location => {
                    const option = document.createElement('option');
                    option.value = location;
                    option.textContent = location;
                    select.appendChild(option);
                });
            }

            // Helper methods
            getStatusConfig(status) {
                const configs = {
                    'baik': { class: 'bg-green-100 text-green-800', text: 'Baik' },
                    'perbaikan': { class: 'bg-yellow-100 text-yellow-800', text: 'Perbaikan' },
                    'rusak': { class: 'bg-red-100 text-red-800', text: 'Rusak' }
                };
                return configs[status] || configs['rusak'];
            }

            getCategoryName(category) {
                const names = {
                    'komputer': 'Komputer',
                    'alat-praktik': 'Alat Praktik',
                    'laptop': 'Laptop',
                    'printer': 'Printer',
                    'jaringan': 'Jaringan',
                    'peripheral': 'Peripheral',
                    'lainnya': 'Lainnya'
                };
                return names[category] || category;
            }

            getTimeAgo(date) {
                const now = new Date();
                const diffMs = now - date;
                const diffMins = Math.floor(diffMs / 60000);
                const diffHours = Math.floor(diffMins / 60);
                const diffDays = Math.floor(diffHours / 24);

                if (diffMins < 60) return `${diffMins} menit lalu`;
                if (diffHours < 24) return `${diffHours} jam lalu`;
                return `${diffDays} hari lalu`;
            }

            refresh() {
                this.updateDashboard();
                this.updateInventoryTable();
                this.updateTransactionTable();
                this.updateStockPage();
                this.updateLocationReports();
                this.populateTransactionItemSelect();
            }
        }

        // Initialize UI
        const ui = new InventoryUI(db);

        // Navigation functions
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => {
                page.classList.add('hidden');
            });
            
            document.getElementById(pageId).classList.remove('hidden');
            document.getElementById(pageId).classList.add('fade-in');
            
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('border-blue-500', 'bg-blue-50', 'text-blue-600');
                btn.classList.add('border-transparent');
            });
            
            event.target.classList.add('border-blue-500', 'bg-blue-50', 'text-blue-600');
            event.target.classList.remove('border-transparent');

            ui.currentPage = pageId;
        }

        // Modal functions
        function showAddItemModal() {
            document.getElementById('addItemModal').classList.remove('hidden');
            document.getElementById('addItemModal').classList.add('flex');
        }

        function hideAddItemModal() {
            document.getElementById('addItemModal').classList.add('hidden');
            document.getElementById('addItemModal').classList.remove('flex');
            document.querySelector('#addItemModal form').reset();
        }

        function showTransactionModal() {
            document.getElementById('transactionModal').classList.remove('hidden');
            document.getElementById('transactionModal').classList.add('flex');
            
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('trans-date').value = today;
            
            ui.populateTransactionItemSelect();
        }

        function hideTransactionModal() {
            document.getElementById('transactionModal').classList.add('hidden');
            document.getElementById('transactionModal').classList.remove('flex');
            document.querySelector('#transactionModal form').reset();
        }

        // Form submission functions
        function addNewItem(event) {
            event.preventDefault();
            
            const formData = new FormData(event.target);
            const itemData = {
                code: document.getElementById('item-code').value,
                name: document.getElementById('item-name').value,
                category: document.getElementById('item-category').value,
                condition: document.getElementById('item-condition').value,
                year: document.getElementById('item-year').value,
                location: document.getElementById('item-location').value,
                quantity: document.getElementById('item-quantity').value
            };

            // Check if code already exists
            const existingItem = db.items.find(item => item.code === itemData.code);
            if (existingItem) {
                showNotification('❌ Kode barang sudah ada!', 'error');
                return;
            }

            const newItem = db.addItem(itemData);
            if (newItem) {
                ui.refresh();
                hideAddItemModal();
                showNotification('✅ Barang berhasil ditambahkan!', 'success');
            } else {
                showNotification('❌ Gagal menambahkan barang!', 'error');
            }
        }

        function addNewTransaction(event) {
            event.preventDefault();
            
            const itemId = document.getElementById('trans-item').value;
            const item = db.items.find(i => i.id === itemId);
            
            if (!item) {
                showNotification('❌ Pilih barang terlebih dahulu!', 'error');
                return;
            }

            const transactionData = {
                date: document.getElementById('trans-date').value,
                type: document.getElementById('trans-type').value,
                itemId: itemId,
                itemName: item.name,
                quantity: document.getElementById('trans-quantity').value,
                note: document.getElementById('trans-note').value
            };

            const newTransaction = db.addTransaction(transactionData);
            if (newTransaction) {
                ui.refresh();
                hideTransactionModal();
                showNotification('✅ Transaksi berhasil dicatat!', 'success');
            } else {
                showNotification('❌ Gagal mencatat transaksi!', 'error');
            }
        }

        // Item management functions
        function editItem(id) {
            const item = db.items.find(i => i.id === id);
            if (item) {
                // Populate form with existing data
                document.getElementById('item-code').value = item.code;
                document.getElementById('item-name').value = item.name;
                document.getElementById('item-category').value = item.category;
                document.getElementById('item-condition').value = item.condition;
                document.getElementById('item-year').value = item.year;
                document.getElementById('item-location').value = item.location;
                document.getElementById('item-quantity').value = item.quantity;
                
                showAddItemModal();
                
                // Change form submission to update instead of add
                const form = document.querySelector('#addItemModal form');
                form.onsubmit = function(event) {
                    event.preventDefault();
                    
                    const updates = {
                        name: document.getElementById('item-name').value,
                        category: document.getElementById('item-category').value,
                        condition: parseInt(document.getElementById('item-condition').value),
                        year: parseInt(document.getElementById('item-year').value),
                        location: document.getElementById('item-location').value,
                        quantity: parseInt(document.getElementById('item-quantity').value)
                    };
                    
                    const updatedItem = db.updateItem(id, updates);
                    if (updatedItem) {
                        ui.refresh();
                        hideAddItemModal();
                        showNotification('✅ Barang berhasil diperbarui!', 'success');
                        
                        // Reset form submission
                        form.onsubmit = addNewItem;
                    } else {
                        showNotification('❌ Gagal memperbarui barang!', 'error');
                    }
                };
            }
        }

        function deleteItem(id) {
            const item = db.items.find(i => i.id === id);
            if (item) {
                // Create custom confirmation dialog
                const confirmDialog = document.createElement('div');
                confirmDialog.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
                confirmDialog.innerHTML = `
                    <div class="bg-white rounded-lg p-6 w-full max-w-md mx-4">
                        <h3 class="text-lg font-semibold text-gray-800 mb-4">🗑️ Konfirmasi Hapus</h3>
                        <p class="text-gray-600 mb-6">Apakah Anda yakin ingin menghapus barang "${item.name}"?</p>
                        <div class="flex justify-end space-x-3">
                            <button onclick="this.closest('.fixed').remove()" class="px-4 py-2 text-gray-600 hover:text-gray-800 transition-colors">
                                Batal
                            </button>
                            <button onclick="confirmDelete('${id}'); this.closest('.fixed').remove()" class="px-4 py-2 bg-red-500 hover:bg-red-600 text-white rounded-md transition-colors">
                                Hapus
                            </button>
                        </div>
                    </div>
                `;
                document.body.appendChild(confirmDialog);
            }
        }

        function confirmDelete(id) {
            const deletedItem = db.deleteItem(id);
            if (deletedItem) {
                ui.refresh();
                showNotification('✅ Barang berhasil dihapus!', 'success');
            } else {
                showNotification('❌ Gagal menghapus barang!', 'error');
            }
        }

        // Report functions
        function generateReport() {
            const stats = db.getStats();
            const transactions = db.getTransactions();
            
            // Update report stats
            document.getElementById('report-in').textContent = transactions.filter(t => t.type === 'masuk').length;
            document.getElementById('report-out').textContent = transactions.filter(t => t.type === 'keluar').length;
            document.getElementById('report-repair').textContent = stats.repair;
            document.getElementById('report-value').textContent = `Rp ${(stats.totalValue / 1000000).toFixed(0)}M`;
            
            // Update detailed report
            const detailedReport = document.getElementById('detailed-report');
            detailedReport.innerHTML = `
                <div>
                    <h4 class="font-medium text-gray-800 mb-3">📊 Ringkasan Transaksi</h4>
                    <div class="space-y-2">
                        <div class="flex justify-between text-sm">
                            <span class="text-gray-600">Total Transaksi:</span>
                            <span class="font-medium">${transactions.length} transaksi</span>
                        </div>
                        <div class="flex justify-between text-sm">
                            <span class="text-gray-600">Rata-rata per Hari:</span>
                            <span class="font-medium">${(transactions.length / 30).toFixed(1)} transaksi</span>
                        </div>
                        <div class="flex justify-between text-sm">
                            <span class="text-gray-600">Kategori Terbanyak:</span>
                            <span class="font-medium">Komputer (${db.getCategoryStats().komputer} unit)</span>
                        </div>
                    </div>
                </div>
                
                <div>
                    <h4 class="font-medium text-gray-800 mb-3">📈 Status Barang</h4>
                    <div class="space-y-2">
                        <div class="flex justify-between text-sm">
                            <span class="text-gray-600">Kondisi Baik:</span>
                            <span class="font-medium text-green-600">${Math.round((stats.available / stats.total) * 100)}%</span>
                        </div>
                        <div class="flex justify-between text-sm">
                            <span class="text-gray-600">Perlu Perbaikan:</span>
                            <span class="font-medium text-yellow-600">${Math.round((stats.repair / stats.total) * 100)}%</span>
                        </div>
                        <div class="flex justify-between text-sm">
                            <span class="text-gray-600">Rusak:</span>
                            <span class="font-medium text-red-600">${Math.round((stats.broken / stats.total) * 100)}%</span>
                        </div>
                    </div>
                </div>
            `;
            
            showNotification('📊 Laporan berhasil di-generate!', 'success');
        }

        function printReport() {
            const stats = db.getStats();
            const month = document.getElementById('report-month').selectedOptions[0].text;
            
            const printWindow = window.open('', '_blank');
            printWindow.document.write(`
                <!DOCTYPE html>
                <html>
                <head>
                    <title>Laporan Inventaris - ${month}</title>
                    <style>
                        body { font-family: Arial, sans-serif; margin: 20px; }
                        .header { text-align: center; margin-bottom: 30px; }
                        .logo { font-size: 24px; font-weight: bold; color: #1f2937; }
                        .subtitle { color: #6b7280; margin-top: 5px; }
                        .report-title { font-size: 20px; font-weight: bold; margin: 20px 0; }
                        .stats-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; margin: 20px 0; }
                        .stat-card { border: 1px solid #e5e7eb; padding: 15px; text-align: center; border-radius: 8px; }
                        .stat-number { font-size: 24px; font-weight: bold; color: #1f2937; }
                        .stat-label { color: #6b7280; font-size: 14px; margin-top: 5px; }
                        .footer { margin-top: 40px; text-align: center; color: #6b7280; font-size: 12px; }
                        @media print { body { margin: 0; } }
                    </style>
                </head>
                <body>
                    <div class="header">
                        <div class="logo">SMK NU 1 ISLAMIYAH KRAMAT</div>
                        <div class="subtitle">💻 Sistem Inventaris Lab Komputer</div>
                        <div class="report-title">Laporan Bulanan - ${month}</div>
                    </div>
                    
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-number">${stats.todayIn}</div>
                            <div class="stat-label">📥 Barang Masuk</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">${stats.todayOut}</div>
                            <div class="stat-label">📤 Barang Keluar</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">${stats.repair}</div>
                            <div class="stat-label">🔧 Perbaikan</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">Rp ${(stats.totalValue / 1000000).toFixed(0)}M</div>
                            <div class="stat-label">💰 Nilai Inventaris</div>
                        </div>
                    </div>
                    
                    <div class="footer">
                        <p>Laporan dicetak pada: ${new Date().toLocaleString('id-ID')}</p>
                        <p>Lab Inventory System v2.0.0 - Ahmad Mashuri, S.Kom</p>
                    </div>
                </body>
                </html>
            `);
            
            printWindow.document.close();
            printWindow.focus();
            setTimeout(() => printWindow.print(), 500);
            
            showNotification('🖨️ Laporan siap dicetak!', 'success');
        }

        // Location report functions
        function filterByLocation() {
            const selectedLocation = document.getElementById('location-filter').value;
            const rows = document.querySelectorAll('#location-report-table tr');
            
            rows.forEach(row => {
                if (!selectedLocation) {
                    row.style.display = '';
                } else {
                    const locationCell = row.cells[0];
                    if (locationCell && locationCell.textContent.includes(selectedLocation)) {
                        row.style.display = '';
                    } else {
                        row.style.display = 'none';
                    }
                }
            });
        }

        function generateLocationReport() {
            ui.updateLocationReports();
            showNotification('📊 Laporan per lokasi berhasil di-generate!', 'success');
        }

        function printLocationReport() {
            const locationStats = db.getLocationStats();
            
            const printWindow = window.open('', '_blank');
            printWindow.document.write(`
                <!DOCTYPE html>
                <html>
                <head>
                    <title>Laporan Per Lokasi</title>
                    <style>
                        body { font-family: Arial, sans-serif; margin: 20px; }
                        .header { text-align: center; margin-bottom: 30px; }
                        .location-cards { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin: 20px 0; }
                        .location-card { border: 1px solid #e5e7eb; padding: 20px; border-radius: 8px; }
                        .footer { margin-top: 40px; text-align: center; color: #6b7280; font-size: 12px; }
                        @media print { body { margin: 0; } }
                    </style>
                </head>
                <body>
                    <div class="header">
                        <h1>SMK NU 1 ISLAMIYAH KRAMAT</h1>
                        <h2>📍 Laporan Per Lokasi</h2>
                    </div>
                    
                    <div class="location-cards">
                        ${Object.entries(locationStats).map(([location, stats]) => `
                            <div class="location-card">
                                <h3>${location}</h3>
                                <p>Total: ${stats.total} unit</p>
                                <p>Baik: ${stats.good} unit</p>
                                <p>Perbaikan: ${stats.repair} unit</p>
                                <p>Rusak: ${stats.broken} unit</p>
                                <p>Kesehatan: ${stats.health}%</p>
                            </div>
                        `).join('')}
                    </div>
                    
                    <div class="footer">
                        <p>Laporan dicetak pada: ${new Date().toLocaleString('id-ID')}</p>
                    </div>
                </body>
                </html>
            `);
            
            printWindow.document.close();
            printWindow.focus();
            setTimeout(() => printWindow.print(), 500);
            
            showNotification('🖨️ Laporan per lokasi siap dicetak!', 'success');
        }

        // Database management functions
        function exportDatabase() {
            const data = db.exportDatabase();
            const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = `inventory_backup_${new Date().toISOString().split('T')[0]}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            showNotification('📤 Database berhasil di-export!', 'success');
        }

        function importDatabase() {
            const input = document.createElement('input');
            input.type = 'file';
            input.accept = '.json';
            
            input.onchange = function(event) {
                const file = event.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        try {
                            const data = JSON.parse(e.target.result);
                            if (db.importDatabase(data)) {
                                ui.refresh();
                                showNotification('📥 Database berhasil di-import!', 'success');
                            } else {
                                showNotification('❌ Gagal import database!', 'error');
                            }
                        } catch (error) {
                            showNotification('❌ File tidak valid!', 'error');
                        }
                    };
                    reader.readAsText(file);
                }
            };
            
            input.click();
        }

        function clearDatabase() {
            // Create custom confirmation dialog
            const confirmDialog = document.createElement('div');
            confirmDialog.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            confirmDialog.innerHTML = `
                <div class="bg-white rounded-lg p-6 w-full max-w-md mx-4">
                    <h3 class="text-lg font-semibold text-gray-800 mb-4">🗑️ Reset Database</h3>
                    <p class="text-gray-600 mb-6">Apakah Anda yakin ingin menghapus semua data? Tindakan ini tidak dapat dibatalkan!</p>
                    <div class="flex justify-end space-x-3">
                        <button onclick="this.closest('.fixed').remove()" class="px-4 py-2 text-gray-600 hover:text-gray-800 transition-colors">
                            Batal
                        </button>
                        <button onclick="confirmClearDatabase(); this.closest('.fixed').remove()" class="px-4 py-2 bg-red-500 hover:bg-red-600 text-white rounded-md transition-colors">
                            Reset
                        </button>
                    </div>
                </div>
            `;
            document.body.appendChild(confirmDialog);
        }

        function confirmClearDatabase() {
            if (db.clearDatabase()) {
                db.initializeData();
                ui.refresh();
                showNotification('🗑️ Database berhasil di-reset!', 'success');
            } else {
                showNotification('❌ Gagal reset database!', 'error');
            }
        }

        // Login System
        function handleLogin(event) {
            event.preventDefault();
            
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const errorDiv = document.getElementById('loginError');
            
            // Check credentials
            if (username === 'admin' && password === 'admin') {
                // Store login session
                sessionStorage.setItem('isLoggedIn', 'true');
                sessionStorage.setItem('loginTime', new Date().toISOString());
                
                // Hide login screen and show main app
                document.getElementById('loginScreen').classList.add('hidden');
                document.getElementById('mainApp').classList.remove('hidden');
                
                // Initialize the application
                ui.refresh();
                
                showNotification('✅ Login berhasil! Selamat datang Admin', 'success');
            } else {
                // Show error message
                errorDiv.classList.remove('hidden');
                document.getElementById('password').value = '';
                
                setTimeout(() => {
                    errorDiv.classList.add('hidden');
                }, 3000);
            }
        }

        function logout() {
            // Create logout confirmation
            const confirmDialog = document.createElement('div');
            confirmDialog.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            confirmDialog.innerHTML = `
                <div class="bg-white rounded-lg p-6 w-full max-w-md mx-4">
                    <h3 class="text-lg font-semibold text-gray-800 mb-4">🚪 Konfirmasi Logout</h3>
                    <p class="text-gray-600 mb-6">Apakah Anda yakin ingin keluar dari sistem?</p>
                    <div class="flex justify-end space-x-3">
                        <button onclick="this.closest('.fixed').remove()" class="px-4 py-2 text-gray-600 hover:text-gray-800 transition-colors">
                            Batal
                        </button>
                        <button onclick="confirmLogout(); this.closest('.fixed').remove()" class="px-4 py-2 bg-red-500 hover:bg-red-600 text-white rounded-md transition-colors">
                            Logout
                        </button>
                    </div>
                </div>
            `;
            document.body.appendChild(confirmDialog);
        }

        function confirmLogout() {
            // Clear session
            sessionStorage.removeItem('isLoggedIn');
            sessionStorage.removeItem('loginTime');
            
            // Show login screen and hide main app
            document.getElementById('mainApp').classList.add('hidden');
            document.getElementById('loginScreen').classList.remove('hidden');
            
            // Clear form
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
            
            showNotification('👋 Logout berhasil! Sampai jumpa', 'success');
        }

        function checkLoginStatus() {
            const isLoggedIn = sessionStorage.getItem('isLoggedIn');
            
            if (isLoggedIn === 'true') {
                // User is logged in, show main app
                document.getElementById('loginScreen').classList.add('hidden');
                document.getElementById('mainApp').classList.remove('hidden');
                ui.refresh();
            } else {
                // User is not logged in, show login screen
                document.getElementById('loginScreen').classList.remove('hidden');
                document.getElementById('mainApp').classList.add('hidden');
            }
        }

        // Notification system
        function showNotification(message, type = 'info') {
            const notification = document.createElement('div');
            notification.className = `fixed top-4 right-4 px-6 py-3 rounded-lg shadow-lg z-50 ${
                type === 'success' ? 'bg-green-500 text-white' : 
                type === 'error' ? 'bg-red-500 text-white' : 
                'bg-blue-500 text-white'
            }`;
            notification.textContent = message;
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.remove();
            }, 3000);
        }

        // Close modals when clicking outside
        document.addEventListener('click', function(event) {
            const addModal = document.getElementById('addItemModal');
            const transModal = document.getElementById('transactionModal');
            
            if (event.target === addModal) {
                hideAddItemModal();
            }
            if (event.target === transModal) {
                hideTransactionModal();
            }
        });

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            checkLoginStatus();
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'991e03c4e509811b',t:'MTc2MTAyMDk3Ni4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
