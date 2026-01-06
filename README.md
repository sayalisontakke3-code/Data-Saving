<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Vendor Display & Analytics Platform</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
            animation: fadeInDown 0.8s ease;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .main-screen {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            animation: fadeInUp 0.8s ease;
        }

        .module-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .module-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            color: white;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .module-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0,0,0,0.3);
        }

        .module-card i {
            font-size: 3em;
            margin-bottom: 15px;
        }

        .module-card h3 {
            font-size: 1.3em;
            margin-bottom: 10px;
        }

        .module-card p {
            font-size: 0.9em;
            opacity: 0.9;
        }

        .page {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .page.active {
            display: block;
        }

        .back-button {
            background: #667eea;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1em;
            margin-bottom: 20px;
            transition: all 0.3s ease;
        }

        .back-button:hover {
            background: #764ba2;
            transform: translateX(-5px);
        }

        .form-container {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 30px;
            margin-top: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }

        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: #667eea;
        }

        .form-group textarea {
            resize: vertical;
            min-height: 100px;
        }

        .submit-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 8px;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
            margin-top: 10px;
        }

        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
        }

        .profile-card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            margin-top: 20px;
        }

        .profile-header {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 2px solid #e0e0e0;
        }

        .profile-image {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            object-fit: cover;
            border: 4px solid #667eea;
        }

        .profile-info {
            flex: 1;
        }

        .profile-info h2 {
            color: #333;
            margin-bottom: 5px;
        }

        .profile-info p {
            color: #666;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .stat-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-card h3 {
            font-size: 2em;
            margin-bottom: 5px;
        }

        .stat-card p {
            opacity: 0.9;
        }

        .display-preview {
            background: #000;
            border-radius: 15px;
            padding: 40px;
            color: white;
            text-align: center;
            margin-top: 20px;
            position: relative;
            overflow: hidden;
        }

        .display-preview::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.1), transparent);
            animation: shine 3s infinite;
        }

        .product-image-preview {
            width: 300px;
            height: 300px;
            object-fit: cover;
            border-radius: 15px;
            margin: 20px auto;
            display: block;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .qr-code {
            width: 150px;
            height: 150px;
            background: white;
            margin: 20px auto;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #333;
            font-weight: bold;
        }

        .analytics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .analytics-card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            border-left: 4px solid #667eea;
        }

        .analytics-card h3 {
            color: #667eea;
            margin-bottom: 10px;
        }

        .analytics-card .value {
            font-size: 2.5em;
            font-weight: bold;
            color: #333;
        }

        .analytics-card .label {
            color: #666;
            margin-top: 5px;
        }

        .data-table {
            width: 100%;
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            margin-top: 20px;
        }

        .data-table table {
            width: 100%;
            border-collapse: collapse;
        }

        .data-table th {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px;
            text-align: left;
        }

        .data-table td {
            padding: 15px;
            border-bottom: 1px solid #e0e0e0;
        }

        .data-table tr:hover {
            background: #f8f9fa;
        }

        .activity-log {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            margin-top: 20px;
            max-height: 500px;
            overflow-y: auto;
        }

        .activity-item {
            padding: 15px;
            border-left: 4px solid #667eea;
            margin-bottom: 15px;
            background: #f8f9fa;
            border-radius: 8px;
        }

        .activity-item .timestamp {
            color: #666;
            font-size: 0.9em;
            margin-bottom: 5px;
        }

        .activity-item .action {
            color: #333;
            font-weight: 600;
        }

        .activity-item .details {
            color: #666;
            font-size: 0.9em;
            margin-top: 5px;
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        @keyframes shine {
            0% {
                transform: translateX(-100%) translateY(-100%);
            }
            100% {
                transform: translateX(100%) translateY(100%);
            }
        }

        .icon {
            font-size: 3em;
            margin-bottom: 15px;
        }

        .quick-actions {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }

        .action-btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 8px;
            background: #667eea;
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .action-btn:hover {
            background: #764ba2;
            transform: translateY(-2px);
        }

        .chart-container {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            margin-top: 20px;
        }

        .badge {
            display: inline-block;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.9em;
            margin: 5px;
        }

        .badge-success {
            background: #4caf50;
            color: white;
        }

        .badge-info {
            background: #2196f3;
            color: white;
        }

        .badge-warning {
            background: #ff9800;
            color: white;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏬 Smart Vendor Display & Analytics Platform</h1>
            <p>Empowering Mall Vendors with Digital Intelligence</p>
        </div>

        <!-- Main Landing Screen -->
        <div id="mainScreen" class="page active">
            <div class="main-screen">
                <h2 style="text-align: center; color: #333; margin-bottom: 30px;">Welcome to Your Control Center</h2>
                <div class="module-grid">
                    <div class="module-card" onclick="navigateTo('vendorDashboard')">
                        <div class="icon">👤</div>
                        <h3>Vendor Dashboard</h3>
                        <p>Manage your profile and view performance metrics</p>
                    </div>
                    <div class="module-card" onclick="navigateTo('displayScreen')">
                        <div class="icon">🖥️</div>
                        <h3>Display Screen</h3>
                        <p>Upload and manage products for digital displays</p>
                    </div>
                    <div class="module-card" onclick="navigateTo('productInfo')">
                        <div class="icon">📊</div>
                        <h3>Product Analytics</h3>
                        <p>Track sales, ratings, and customer engagement</p>
                    </div>
                    <div class="module-card" onclick="navigateTo('customerData')">
                        <div class="icon">👥</div>
                        <h3>Customer Data</h3>
                        <p>View detailed transaction and behavior records</p>
                    </div>
                </div>
                
                <div style="margin-top: 40px; text-align: center;">
                    <button class="submit-btn" onclick="navigateTo('activityLog')" style="width: auto; padding: 15px 40px;">
                        📋 View Activity Log & System Tracking
                    </button>
                </div>
            </div>
        </div>

        <!-- Vendor Dashboard -->
        <div id="vendorDashboard" class="page">
            <div class="main-screen">
                <button class="back-button" onclick="navigateTo('mainScreen')">← Back to Home</button>
                <h2 style="color: #333; margin-bottom: 20px;">Vendor Dashboard</h2>
                
                <div class="form-container">
                    <form id="vendorForm">
                        <div class="form-group">
                            <label>Vendor Name *</label>
                            <input type="text" id="vendorName" required placeholder="Enter your full name">
                        </div>
                        <div class="form-group">
                            <label>Shop Name *</label>
                            <input type="text" id="shopName" required placeholder="Enter shop name">
                        </div>
                        <div class="form-group">
                            <label>Shop Number *</label>
                            <input type="text" id="shopNumber" required placeholder="e.g., A-123">
                        </div>
                        <div class="form-group">
                            <label>Mall Name *</label>
                            <input type="text" id="mallName" required placeholder="Enter mall name">
                        </div>
                        <div class="form-group">
                            <label>Monthly Sales Performance (₹) *</label>
                            <input type="number" id="monthlyPerformance" required placeholder="Enter monthly sales">
                        </div>
                        <div class="form-group">
                            <label>Vendor Photo</label>
                            <input type="file" id="vendorPhoto" accept="image/*" onchange="previewImage(event, 'vendorPhotoPreview')">
                            <img id="vendorPhotoPreview" style="max-width: 200px; margin-top: 10px; border-radius: 10px; display: none;">
                        </div>
                        <button type="submit" class="submit-btn">Save Vendor Details</button>
                    </form>
                </div>
            </div>
        </div>

        <!-- Vendor Profile -->
        <div id="vendorProfile" class="page">
            <div class="main-screen">
                <button class="back-button" onclick="navigateTo('vendorDashboard')">← Back to Dashboard</button>
                <h2 style="color: #333; margin-bottom: 20px;">Vendor Profile</h2>
                
                <div class="profile-card">
                    <div class="profile-header">
                        <img id="profileImage" src="https://via.placeholder.com/100" alt="Vendor" class="profile-image">
                        <div class="profile-info">
                            <h2 id="profileName">Vendor Name</h2>
                            <p id="profileShop">Shop Name</p>
                            <p id="profileLocation">Shop Number | Mall Name</p>
                        </div>
                    </div>
                    
                    <div class="stats-grid">
                        <div class="stat-card">
                            <h3 id="profileSales">₹0</h3>
                            <p>Monthly Sales</p>
                        </div>
                        <div class="stat-card">
                            <h3 id="profileProducts">0</h3>
                            <p>Products Listed</p>
                        </div>
                        <div class="stat-card">
                            <h3 id="profileDisplays">0</h3>
                            <p>Active Displays</p>
                        </div>
                    </div>
                    
                    <div class="quick-actions">
                        <button class="action-btn" onclick="navigateTo('displayScreen')">➕ Add Product</button>
                        <button class="action-btn" onclick="navigateTo('productInfo')">📊 View Analytics</button>
                        <button class="action-btn" onclick="navigateTo('customerData')">👥 Customer Data</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Display Screen Management -->
        <div id="displayScreen" class="page">
            <div class="main-screen">
                <button class="back-button" onclick="navigateTo('mainScreen')">← Back to Home</button>
                <h2 style="color: #333; margin-bottom: 20px;">Display Screen Management</h2>
                
                <div class="form-container">
                    <form id="productForm">
                        <div class="form-group">
                            <label>Product Name *</label>
                            <input type="text" id="productName" required placeholder="Enter product name">
                        </div>
                        <div class="form-group">
                            <label>Product Image *</label>
                            <input type="file" id="productImage" accept="image/*" required onchange="previewImage(event, 'productImagePreview')">
                            <img id="productImagePreview" style="max-width: 300px; margin-top: 10px; border-radius: 10px; display: none;">
                        </div>
                        <div class="form-group">
                            <label>Product Description *</label>
                            <textarea id="productDescription" required placeholder="Describe your product..."></textarea>
                        </div>
                        <div class="form-group">
                            <label>Price (₹) *</label>
                            <input type="number" id="productPrice" required placeholder="Enter price">
                        </div>
                        <div class="form-group">
                            <label>Discount (%) *</label>
                            <input type="number" id="productDiscount" required placeholder="Enter discount percentage" min="0" max="100">
                        </div>
                        <div class="form-group">
                            <label>Initial Rating (1-5) *</label>
                            <input type="number" id="productRating" required placeholder="Enter rating" min="1" max="5" step="0.1">
                        </div>
                        <div class="form-group">
                            <label>Product URL / Shop Website *</label>
                            <input type="url" id="productUrl" required placeholder="https://yourshop.com/product">
                        </div>
                        <button type="submit" class="submit-btn">Save Product & Go Live</button>
                    </form>
                </div>
            </div>
        </div>

        <!-- Display Preview -->
        <div id="displayPreview" class="page">
            <div class="main-screen">
                <button class="back-button" onclick="navigateTo('displayScreen')">← Back to Product Upload</button>
                <h2 style="color: #333; margin-bottom: 20px;">🎉 Product Live on Display!</h2>
                
                <div class="display-preview">
                    <h1 id="displayProductName" style="font-size: 2.5em; margin-bottom: 20px;">Product Name</h1>
                    <img id="displayProductImage" src="" alt="Product" class="product-image-preview">
                    <p id="displayProductDesc" style="font-size: 1.2em; margin: 20px 0; opacity: 0.9;">Product description will appear here</p>
                    <div style="display: flex; justify-content: center; gap: 40px; margin: 20px 0;">
                        <div>
                            <p style="font-size: 1.5em; opacity: 0.8;">Price</p>
                            <h2 id="displayPrice" style="font-size: 3em;">₹0</h2>
                        </div>
                        <div>
                            <p style="font-size: 1.5em; opacity: 0.8;">Discount</p>
                            <h2 id="displayDiscount" style="font-size: 3em; color: #4caf50;">0%</h2>
                        </div>
                        <div>
                            <p style="font-size: 1.5em; opacity: 0.8;">Rating</p>
                            <h2 id="displayRating" style="font-size: 3em; color: #ffd700;">⭐ 0</h2>
                        </div>
                    </div>
                    <div class="qr-code">
                        <div style="text-align: center;">
                            <div style="font-size: 3em;">📱</div>
                            <p style="margin-top: 10px;">QR Code</p>
                            <p style="font-size: 0.8em;">Scan to Buy</p>
                        </div>
                    </div>
                    <p style="margin-top: 20px; font-size: 1.5em;">👆 Scan to Purchase Instantly!</p>
                </div>
            </div>
        </div>

        <!-- Product Analytics -->
        <div id="productInfo" class="page">
            <div class="main-screen">
                <button class="back-button" onclick="navigateTo('mainScreen')">← Back to Home</button>
                <h2 style="color: #333; margin-bottom: 20px;">Product Analytics Dashboard</h2>
                
                <div class="analytics-grid">
                    <div class="analytics-card">
                        <h3>Today's Sales</h3>
                        <div class="value" id="todaySales">0</div>
                        <div class="label">Customers Purchased</div>
                    </div>
                    <div class="analytics-card">
                        <h3>QR Code Scans</h3>
                        <div class="value" id="qrScans">0</div>
                        <div class="label">Today's Engagements</div>
                    </div>
                    <div class="analytics-card">
                        <h3>New Ratings</h3>
                        <div class="value" id="newRatings">0</div>
                        <div class="label">Received Today</div>
                    </div>
                    <div class="analytics-card">
                        <h3>Conversion Rate</h3>
                        <div class="value" id="conversionRate">0%</div>
                        <div class="label">Scans to Purchase</div>
                    </div>
                </div>
                
                <div class="chart-container">
                    <h3 style="color: #333; margin-bottom: 20px;">🏆 Today's Highest Sold Product</h3>
                    <div id="topProduct" style="text-align: center; padding: 20px;">
                        <h2 style="color: #667eea; font-size: 2em;">No sales data yet</h2>
                        <p style="color: #666; margin-top: 10px;">Start selling to see top products!</p>
                    </div>
                </div>
                
                <div class="chart-container">
                    <h3 style="color: #333; margin-bottom: 20px;">📈 Sales Timeline (Last 7 Days)</h3>
                    <div style="text-align: center; padding: 40px; color: #666;">
                        <p>Interactive sales chart will be displayed here</p>
                        <div style="margin-top: 20px; display: flex; justify-content: space-around;">
                            <div><strong>Mon:</strong> 12 sales</div>
                            <div><strong>Tue:</strong> 18 sales</div>
                            <div><strong>Wed:</strong> 15 sales</div>
                            <div><strong>Thu:</strong> 22 sales</div>
                            <div><strong>Fri:</strong> 28 sales</div>
                            <div><strong>Sat:</strong> 35 sales</div>
                            <div><strong>Sun:</strong> 30 sales</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Customer Data -->
        <div id="customerData" class="page">
            <div class="main-screen">
                <button class="back-button" onclick="navigateTo('mainScreen')">← Back to Home</button>
                <h2 style="color: #333; margin-bottom: 20px;">Customer Transaction Records</h2>
                
                <div class="data-table">
                    <table>
                        <thead>
                            <tr>
                                <th>Customer ID</th>
                                <th>Product</th>
                                <th>Date & Time</th>
                                <th>Quantity</th>
                                <th>Discount</th>
                                <th>Payment</th>
                                <th>Delivery</th>
                                <th>Time Slot</th>
                            </tr>
                        </thead>
                        <tbody id="customerTableBody">
                            <tr>
                                <td colspan="8" style="text-align: center; padding: 40px; color: #666;">
                                    No transaction data available yet. Data will appear automatically when customers make purchases.
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                
                <div style="margin-top: 20px; padding: 20px; background: #f8f9fa; border-radius: 10px;">
                    <h3 style="color: #333; margin-bottom: 10px;">📊 Quick Stats</h3>
                    <div style="display: flex; gap: 20px; flex-wrap: wrap;">
                        <div><span class="badge badge-success">Total Customers: <strong id="totalCustomers">0</strong></span></div>
                        <div><span class="badge badge-info">Total Orders: <strong id="totalOrders">0</strong></span></div>
                        <div><span class="badge badge-warning">Total Revenue: <strong id="totalRevenue">₹0</strong></span></div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Activity Log -->
        <div id="activityLog" class="page">
            <div class="main-screen">
                <button class="back-button" onclick="navigateTo('mainScreen')">← Back to Home</button>
                <h2 style="color: #333; margin-bottom: 20px;">🔍 Activity Log & Movement Tracking</h2>
                
                <div style="background: #f8f9fa; padding: 20px; border-radius: 10px; margin-bottom: 20px;">
                    <h3 style="color: #333; margin-bottom: 10px;">What Gets Tracked:</h3>
                    <div style="display: flex; flex-wrap: wrap; gap: 10px;">
                        <span class="badge badge-info">Vendor Login/Logout</span>
                        <span class="badge badge-info">Product Added/Edited</span>
                        <span class="badge badge-info">Display Updates</span>
                        <span class="badge badge-success">QR Code Scans</span>
                        <span class="badge badge-success">Product Views</span>
                        <span class="badge badge-success">Purchases</span>
                        <span class="badge badge-warning">Payment Completed</span>
                        <span class="badge badge-warning">Ratings Submitted</span>
                    </div>
                </div>
                
                <div class="activity-log" id="activityLogContainer">
                    <!-- Activity items will be dynamically added here -->
                    <div class="activity-item">
                        <div class="timestamp">🕐 Just now</div>
                        <div class="action">System Initialized</div>
                        <div class="details">Activity tracking system is now active and recording all movements</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Global data storage
        let vendorData = {};
        let products = [];
        let customers = [];
        let activityLog = [];

        // Navigation function
        function navigateTo(pageId) {
            // Hide all pages
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            
            // Show selected page
            document.getElementById(pageId).classList.add('active');
            
            // Log activity
            logActivity('navigation', `Navigated to ${pageId}`);
            
            // Scroll to top
            window.scrollTo(0, 0);
        }

        // Image preview function
        function previewImage(event, previewId) {
            const file = event.target.files[0];
            const preview = document.getElementById(previewId);
            
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    preview.src = e.target.result;
                    preview.style.display = 'block';
                }
                reader.readAsDataURL(file);
            }
        }

        // Activity logging function
        function logActivity(type, action, details = '') {
            const timestamp = new Date().toLocaleString();
            const activity = {
                timestamp: timestamp,
                type: type,
                action: action,
                details: details
            };
            
            activityLog.push(activity);
            updateActivityLog();
        }

        // Update activity log display
        function updateActivityLog() {
            const container = document.getElementById('activityLogContainer');
            const latestActivities = activityLog.slice(-20).reverse(); // Show last 20 activities
            
            container.innerHTML = latestActivities.map(activity => `
                <div class="activity-item">
                    <div class="timestamp">🕐 ${activity.timestamp}</div>
                    <div class="action">${activity.action}</div>
                    ${activity.details ? `<div class="details">${activity.details}</div>` : ''}
                </div>
            `).join('');
        }

        // Vendor form submission
        document.getElementById('vendorForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            vendorData = {
                name: document.getElementById('vendorName').value,
                shopName: document.getElementById('shopName').value,
                shopNumber: document.getElementById('shopNumber').value,
                mallName: document.getElementById('mallName').value,
                monthlyPerformance: document.getElementById('monthlyPerformance').value,
                photo: document.getElementById('vendorPhotoPreview').src
            };
            
            // Update profile page
            document.getElementById('profileName').textContent = vendorData.name;
            document.getElementById('profileShop').textContent = vendorData.shopName;
            document.getElementById('profileLocation').textContent = `${vendorData.shopNumber} | ${vendorData.mallName}`;
            document.getElementById('profileSales').textContent = `₹${parseFloat(vendorData.monthlyPerformance).toLocaleString()}`;
            document.getElementById('profileProducts').textContent = products.length;
            document.getElementById('profileDisplays').textContent = products.length;
            
            if (vendorData.photo && vendorData.photo !== 'https://via.placeholder.com/100') {
                document.getElementById('profileImage').src = vendorData.photo;
            }
            
            // Log activity
            logActivity('vendor', 'Vendor Profile Created', `${vendorData.name} - ${vendorData.shopName}`);
            
            // Navigate to profile
            navigateTo('vendorProfile');
        });

        // Product form submission
        document.getElementById('productForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const product = {
                id: Date.now(),
                name: document.getElementById('productName').value,
                image: document.getElementById('productImagePreview').src,
                description: document.getElementById('productDescription').value,
                price: parseFloat(document.getElementById('productPrice').value),
                discount: parseFloat(document.getElementById('productDiscount').value),
                rating: parseFloat(document.getElementById('productRating').value),
                url: document.getElementById('productUrl').value,
                sales: 0,
                scans: 0,
                ratings: 0
            };
            
            products.push(product);
            
            // Update display preview
            document.getElementById('displayProductName').textContent = product.name;
            document.getElementById('displayProductImage').src = product.image;
            document.getElementById('displayProductDesc').textContent = product.description;
            document.getElementById('displayPrice').textContent = `₹${product.price.toLocaleString()}`;
            document.getElementById('displayDiscount').textContent = `${product.discount}%`;
            document.getElementById('displayRating').textContent = `⭐ ${product.rating}`;
            
            // Update profile stats
            document.getElementById('profileProducts').textContent = products.length;
            document.getElementById('profileDisplays').textContent = products.length;
            
            // Log activity
            logActivity('product', 'New Product Added to Display', `${product.name} - ₹${product.price}`);
            
            // Simulate some activity for demo
            setTimeout(() => {
                simulateActivity(product);
            }, 2000);
            
            // Navigate to preview
            navigateTo('displayPreview');
            
            // Reset form
            document.getElementById('productForm').reset();
            document.getElementById('productImagePreview').style.display = 'none';
        });

        // Simulate customer activity for demo purposes
        function simulateActivity(product) {
            // Simulate QR scan
            product.scans++;
            logActivity('customer', 'QR Code Scanned', `Product: ${product.name} | Display Screen #${Math.floor(Math.random() * 5) + 1}`);
            
            setTimeout(() => {
                // Simulate purchase
                if (Math.random() > 0.3) { // 70% conversion
                    product.sales++;
                    
                    const customer = {
                        id: `CUST-${Date.now()}`,
                        product: product.name,
                        datetime: new Date().toLocaleString(),
                        quantity: Math.floor(Math.random() * 3) + 1,
                        discount: product.discount,
                        payment: ['UPI', 'Card', 'Scanner'][Math.floor(Math.random() * 3)],
                        delivery: ['Home Delivery', 'Store Pickup'][Math.floor(Math.random() * 2)],
                        timeSlot: ['10AM-12PM', '2PM-4PM', '6PM-8PM'][Math.floor(Math.random() * 3)]
                    };
                    
                    customers.push(customer);
                    logActivity('purchase', 'Purchase Completed', `${customer.id} bought ${customer.quantity}x ${product.name} via ${customer.payment}`);
                    
                    // Update customer table
                    updateCustomerTable();
                    
                    // Simulate rating
                    setTimeout(() => {
                        product.ratings++;
                        logActivity('rating', 'Product Rated', `${product.name} received a ${(Math.random() * 2 + 3).toFixed(1)} ⭐ rating`);
                        updateAnalytics();
                    }, 1000);
                } else {
                    logActivity('customer', 'Product Viewed', `Customer viewed ${product.name} but did not purchase`);
                }
                
                updateAnalytics();
            }, 1500);
        }

        // Update analytics dashboard
        function updateAnalytics() {
            const todaySales = products.reduce((sum, p) => sum + p.sales, 0);
            const qrScans = products.reduce((sum, p) => sum + p.scans, 0);
            const newRatings = products.reduce((sum, p) => sum + p.ratings, 0);
            const conversionRate = qrScans > 0 ? ((todaySales / qrScans) * 100).toFixed(1) : 0;
            
            document.getElementById('todaySales').textContent = todaySales;
            document.getElementById('qrScans').textContent = qrScans;
            document.getElementById('newRatings').textContent = newRatings;
            document.getElementById('conversionRate').textContent = `${conversionRate}%`;
            
            // Find top product
            const topProduct = products.reduce((max, p) => p.sales > max.sales ? p : max, { sales: 0, name: 'No sales yet' });
            
            if (topProduct.sales > 0) {
                document.getElementById('topProduct').innerHTML = `
                    <h2 style="color: #667eea; font-size: 2em;">${topProduct.name}</h2>
                    <p style="color: #666; margin-top: 10px; font-size: 1.2em;">${topProduct.sales} units sold | ${topProduct.scans} scans | ${topProduct.ratings} ratings</p>
                `;
            }
        }

        // Update customer data table
        function updateCustomerTable() {
            const tbody = document.getElementById('customerTableBody');
            
            if (customers.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="8" style="text-align: center; padding: 40px; color: #666;">
                            No transaction data available yet. Data will appear automatically when customers make purchases.
                        </td>
                    </tr>
                `;
            } else {
                tbody.innerHTML = customers.map(customer => `
                    <tr>
                        <td>${customer.id}</td>
                        <td>${customer.product}</td>
                        <td>${customer.datetime}</td>
                        <td>${customer.quantity}</td>
                        <td>${customer.discount}%</td>
                        <td>${customer.payment}</td>
                        <td>${customer.delivery}</td>
                        <td>${customer.timeSlot}</td>
                    </tr>
                `).join('');
                
                // Update stats
                document.getElementById('totalCustomers').textContent = customers.length;
                document.getElementById('totalOrders').textContent = customers.length;
                const totalRevenue = customers.reduce((sum, c) => {
                    const product = products.find(p => p.name === c.product);
                    return sum + (product ? product.price * c.quantity : 0);
                }, 0);
                document.getElementById('totalRevenue').textContent = `₹${totalRevenue.toLocaleString()}`;
            }
        }

        // Initialize activity log
        logActivity('system', 'Platform Initialized', 'Smart Vendor Display & Analytics Platform is ready');
        
        // Simulate some initial activity after 3 seconds
        setTimeout(() => {
            logActivity('system', 'Display Screens Connected', '5 digital screens are online and ready');
        }, 3000);
    </script>
</body>
</html>
