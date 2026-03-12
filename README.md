<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Library Management System</title>
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
            background: white;
            border-radius: 15px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .header {
            background: #2c3e50;
            color: white;
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .header h1 {
            font-size: 24px;
        }

        .chart-link {
            background: #3498db;
            color: white;
            padding: 10px 20px;
            border-radius: 5px;
            text-decoration: none;
            transition: background 0.3s;
        }

        .chart-link:hover {
            background: #2980b9;
        }

        .nav-bar {
            background: #34495e;
            padding: 10px 20px;
            display: flex;
            gap: 20px;
        }

        .nav-btn {
            background: none;
            border: none;
            color: white;
            padding: 10px 20px;
            cursor: pointer;
            font-size: 16px;
            border-radius: 5px;
            transition: background 0.3s;
        }

        .nav-btn:hover {
            background: #2c3e50;
        }

        .nav-btn.active {
            background: #3498db;
        }

        .content {
            padding: 30px;
            min-height: 500px;
        }

        .form-container {
            max-width: 800px;
            margin: 0 auto;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #333;
        }

        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 10px;
            border: 2px solid #e0e0e0;
            border-radius: 5px;
            font-size: 16px;
            transition: border-color 0.3s;
        }

        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            outline: none;
            border-color: #3498db;
        }

        .form-group input[type="password"] {
            font-family: 'password';
        }

        .radio-group, .checkbox-group {
            display: flex;
            gap: 20px;
            align-items: center;
        }

        .radio-group label, .checkbox-group label {
            display: inline;
            margin-left: 5px;
            font-weight: normal;
        }

        .error-message {
            background: #e74c3c;
            color: white;
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 20px;
            display: none;
        }

        .success-message {
            background: #27ae60;
            color: white;
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 20px;
            display: none;
        }

        .btn-group {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }

        .btn {
            padding: 12px 30px;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            transition: background 0.3s;
        }

        .btn-primary {
            background: #3498db;
            color: white;
        }

        .btn-primary:hover {
            background: #2980b9;
        }

        .btn-secondary {
            background: #95a5a6;
            color: white;
        }

        .btn-secondary:hover {
            background: #7f8c8d;
        }

        .table-container {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #db9797;
        }

        th {
            background: #f8f9fa;
            font-weight: 600;
            color: #8a7474;
        }

        tr:hover {
            background: #f8f9fa;
        }

        .login-container {
            max-width: 400px;
            margin: 50px auto;
            padding: 30px;
            background: #f8f9fa;
            border-radius: 10px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
        }

        .login-container h2 {
            margin-bottom: 20px;
            color: #333;
            text-align: center;
        }

        .role-info {
            margin-top: 20px;
            padding: 15px;
            background: #e8f4fd;
            border-radius: 5px;
            font-size: 14px;
        }

        .role-info p {
            margin: 5px 0;
            color: #a9c2db;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
        }

        .modal-content {
            position: relative;
            background: white;
            margin: 50px auto;
            padding: 20px;
            width: 90%;
            max-width: 600px;
            border-radius: 10px;
            max-height: 80vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .close-modal {
            font-size: 24px;
            cursor: pointer;
            color: #e2dfdf;
        }

        .close-modal:hover {
            color: #161616;
        }

        .chart-image {
            width: 100%;
            height: auto;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📚 Library Management System</h1>
            <a href="#" class="chart-link" onclick="showChart()">View System Flow Chart</a>
        </div>

        <div class="nav-bar" id="mainNav">
            <button class="nav-btn active" onclick="showLogin()">Login</button>
            <button class="nav-btn" onclick="showDashboard()" id="dashboardBtn" style="display:none;">Dashboard</button>
            <button class="nav-btn" onclick="showMaintenance()" id="maintenanceBtn" style="display:none;">Maintenance</button>
            <button class="nav-btn" onclick="showReports()" id="reportsBtn" style="display:none;">Reports</button>
            <button class="nav-btn" onclick="showTransactions()" id="transactionsBtn" style="display:none;">Transactions</button>
            <button class="nav-btn" onclick="logout()" id="logoutBtn" style="display:none;">Logout</button>
        </div>

        <div class="content" id="contentArea">
            <!-- Login Form -->
            <div id="loginForm" class="login-container">
                <h2>Login to Library System</h2>
                <div class="error-message" id="loginError"></div>
                <div class="form-group">
                    <label>User ID:</label>
                    <input type="text" id="userId" placeholder="Enter User ID">
                </div>
                <div class="form-group">
                    <label>Password:</label>
                    <input type="password" id="password" placeholder="Enter Password">
                </div>
                <div class="btn-group">
                    <button class="btn btn-primary" onclick="login()">Login</button>
                    <button class="btn btn-secondary" onclick="clearLogin()">Cancel</button>
                </div>
                <div class="role-info">
                    <p><strong>Demo Credentials:</strong></p>
                    <p>Admin: admin / admin123</p>
                    <p>User: user / user123</p>
                </div>
            </div>

            <!-- Dashboard -->
            <div id="dashboard" style="display:none;">
                <h2>Dashboard</h2>
                <p>Welcome to the Library Management System</p>
                <div class="table-container">
                    <table>
                        <tr>
                            <th>Module</th>
                            <th>Description</th>
                            <th>Access</th>
                        </tr>
                        <tr>
                            <td>Maintenance</td>
                            <td>Manage memberships, books, and users</td>
                            <td id="maintenanceAccess">Admin Only</td>
                        </tr>
                        <tr>
                            <td>Reports</td>
                            <td>View various reports</td>
                            <td id="reportsAccess">All Users</td>
                        </tr>
                        <tr>
                            <td>Transactions</td>
                            <td>Issue, return books, and pay fines</td>
                            <td id="transactionsAccess">All Users</td>
                        </tr>
                    </table>
                </div>
            </div>

            <!-- Maintenance Module -->
            <div id="maintenance" style="display:none;">
                <h2>Maintenance Module</h2>
                <div class="btn-group">
                    <button class="btn btn-primary" onclick="showAddMembership()">Add Membership</button>
                    <button class="btn btn-primary" onclick="showUpdateMembership()">Update Membership</button>
                    <button class="btn btn-primary" onclick="showUserManagement()">User Management</button>
                    <button class="btn btn-primary" onclick="showAddBook()">Add Book</button>
                    <button class="btn btn-primary" onclick="showUpdateBook()">Update Book</button>
                </div>
                <div id="maintenanceContent"></div>
            </div>

            <!-- Reports Module -->
            <div id="reports" style="display:none;">
                <h2>Reports Module</h2>
                <div class="btn-group">
                    <button class="btn btn-primary" onclick="showBookAvailability()">Book Availability</button>
                    <button class="btn btn-primary" onclick="showIssuedBooks()">Issued Books</button>
                    <button class="btn btn-primary" onclick="showOverdueBooks()">Overdue Books</button>
                    <button class="btn btn-primary" onclick="showMembershipReport()">Membership Report</button>
                </div>
                <div id="reportsContent"></div>
            </div>

            <!-- Transactions Module -->
            <div id="transactions" style="display:none;">
                <h2>Transactions Module</h2>
                <div class="btn-group">
                    <button class="btn btn-primary" onclick="showBookIssue()">Book Issue</button>
                    <button class="btn btn-primary" onclick="showReturnBook()">Return Book</button>
                    <button class="btn btn-primary" onclick="showPayFine()">Pay Fine</button>
                    <button class="btn btn-primary" onclick="showSearchResults()">Search Books</button>
                </div>
                <div id="transactionsContent"></div>
            </div>
        </div>
    </div>

    <!-- Chart Modal -->
    <div id="chartModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>System Flow Chart</h2>
                <span class="close-modal" onclick="closeChart()">&times;</span>
            </div>
            <div class="chart-image">
                <pre style="font-family: monospace; white-space: pre; overflow-x: auto;">

                </pre>
            </div>
        </div>
    </div>

    <script>
        // Global variables
        let currentUser = null;
        let currentRole = null;
        let books = [
            { id: 1, name: 'The Great Gatsby', author: 'F. Scott Fitzgerald', available: true, serialNo: 'BK001' },
            { id: 2, name: 'To Kill a Mockingbird', author: 'Harper Lee', available: true, serialNo: 'BK002' },
            { id: 3, name: '1984', author: 'George Orwell', available: true, serialNo: 'BK003' },
            { id: 4, name: 'Pride and Prejudice', author: 'Jane Austen', available: false, serialNo: 'BK004' },
            { id: 5, name: 'The Catcher in the Rye', author: 'J.D. Salinger', available: true, serialNo: 'BK005' }
        ];
        let members = [
            { id: 1, name: 'John Doe', address: '123 Main St', phone: '555-0100', email: 'john@example.com', membership: '6 months' },
            { id: 2, name: 'Jane Smith', address: '456 Oak Ave', phone: '555-0200', email: 'jane@example.com', membership: '1 year' }
        ];
        let issuedBooks = [];
        let fines = [];

        // Login function
        function login() {
            const userId = document.getElementById('userId').value;
            const password = document.getElementById('password').value;
            const loginError = document.getElementById('loginError');

            if (!userId || !password) {
                showError(loginError, 'Please enter both User ID and Password');
                return;
            }

            // Simple authentication (for demo purposes)
            if (userId === 'admin' && password === 'admin123') {
                currentUser = 'Admin';
                currentRole = 'admin';
                loginSuccess();
            } else if (userId === 'user' && password === 'user123') {
                currentUser = 'User';
                currentRole = 'user';
                loginSuccess();
            } else {
                showError(loginError, 'Invalid User ID or Password');
            }
        }

        function loginSuccess() {
            document.getElementById('loginForm').style.display = 'none';
            document.getElementById('dashboard').style.display = 'block';
            document.getElementById('dashboardBtn').style.display = 'block';
            document.getElementById('logoutBtn').style.display = 'block';
            
            // Show/hide maintenance button based on role
            if (currentRole === 'admin') {
                document.getElementById('maintenanceBtn').style.display = 'block';
                document.getElementById('maintenanceAccess').textContent = 'Admin Only';
            } else {
                document.getElementById('maintenanceBtn').style.display = 'none';
                document.getElementById('maintenanceAccess').textContent = 'No Access';
            }
            
            document.getElementById('reportsBtn').style.display = 'block';
            document.getElementById('transactionsBtn').style.display = 'block';
            
            updateNavButtons('dashboard');
        }

        function logout() {
            currentUser = null;
            currentRole = null;
            document.getElementById('loginForm').style.display = 'block';
            document.getElementById('dashboard').style.display = 'none';
            document.getElementById('maintenance').style.display = 'none';
            document.getElementById('reports').style.display = 'none';
            document.getElementById('transactions').style.display = 'none';
            
            document.getElementById('dashboardBtn').style.display = 'none';
            document.getElementById('maintenanceBtn').style.display = 'none';
            document.getElementById('reportsBtn').style.display = 'none';
            document.getElementById('transactionsBtn').style.display = 'none';
            document.getElementById('logoutBtn').style.display = 'none';
            
            document.getElementById('userId').value = '';
            document.getElementById('password').value = '';
        }

        function clearLogin() {
            document.getElementById('userId').value = '';
            document.getElementById('password').value = '';
            document.getElementById('loginError').style.display = 'none';
        }

        function showError(element, message) {
            element.textContent = message;
            element.style.display = 'block';
            setTimeout(() => {
                element.style.display = 'none';
            }, 3000);
        }

        function showSuccess(message) {
            const successDiv = document.createElement('div');
            successDiv.className = 'success-message';
            successDiv.textContent = message;
            successDiv.style.display = 'block';
            
            const contentArea = document.getElementById('contentArea');
            contentArea.insertBefore(successDiv, contentArea.firstChild);
            
            setTimeout(() => {
                successDiv.remove();
            }, 3000);
        }

        function updateNavButtons(active) {
            const buttons = document.querySelectorAll('.nav-btn');
            buttons.forEach(btn => {
                btn.classList.remove('active');
                if (btn.textContent.toLowerCase().includes(active)) {
                    btn.classList.add('active');
                }
            });
        }

        function showLogin() {
            if (!currentUser) {
                document.getElementById('loginForm').style.display = 'block';
                document.getElementById('dashboard').style.display = 'none';
                document.getElementById('maintenance').style.display = 'none';
                document.getElementById('reports').style.display = 'none';
                document.getElementById('transactions').style.display = 'none';
            }
            updateNavButtons('login');
        }

        function showDashboard() {
            if (currentUser) {
                document.getElementById('loginForm').style.display = 'none';
                document.getElementById('dashboard').style.display = 'block';
                document.getElementById('maintenance').style.display = 'none';
                document.getElementById('reports').style.display = 'none';
                document.getElementById('transactions').style.display = 'none';
                updateNavButtons('dashboard');
            }
        }

        function showMaintenance() {
            if (currentRole === 'admin') {
                document.getElementById('loginForm').style.display = 'none';
                document.getElementById('dashboard').style.display = 'none';
                document.getElementById('maintenance').style.display = 'block';
                document.getElementById('reports').style.display = 'none';
                document.getElementById('transactions').style.display = 'none';
                updateNavButtons('maintenance');
            } else {
                showError(document.createElement('div'), 'Access Denied: Admin only');
            }
        }

        function showReports() {
            if (currentUser) {
                document.getElementById('loginForm').style.display = 'none';
                document.getElementById('dashboard').style.display = 'none';
                document.getElementById('maintenance').style.display = 'none';
                document.getElementById('reports').style.display = 'block';
                document.getElementById('transactions').style.display = 'none';
                updateNavButtons('reports');
                showBookAvailability();
            }
        }

        function showTransactions() {
            if (currentUser) {
                document.getElementById('loginForm').style.display = 'none';
                document.getElementById('dashboard').style.display = 'none';
                document.getElementById('maintenance').style.display = 'none';
                document.getElementById('reports').style.display = 'none';
                document.getElementById('transactions').style.display = 'block';
                updateNavButtons('transactions');
                showBookIssue();
            }
        }

        // Chart functions
        function showChart() {
            document.getElementById('chartModal').style.display = 'block';
        }

        function closeChart() {
            document.getElementById('chartModal').style.display = 'none';
        }

        // Maintenance Functions
        function showAddMembership() {
            if (currentRole !== 'admin') return;
            
            const content = document.getElementById('maintenanceContent');
            content.innerHTML = `
                <h3>Add Membership</h3>
                <div class="form-container">
                    <div class="error-message" id="membershipError"></div>
                    <div class="form-group">
                        <label>Name:</label>
                        <input type="text" id="memName" required>
                    </div>
                    <div class="form-group">
                        <label>Address:</label>
                        <input type="text" id="memAddress" required>
                    </div>
                    <div class="form-group">
                        <label>Phone:</label>
                        <input type="text" id="memPhone" required>
                    </div>
                    <div class="form-group">
                        <label>Email:</label>
                        <input type="email" id="memEmail" required>
                    </div>
                    <div class="form-group">
                        <label>Membership Duration:</label>
                        <div class="radio-group">
                            <input type="radio" name="duration" id="duration6" value="6 months" checked>
                            <label for="duration6">6 months</label>
                            <input type="radio" name="duration" id="duration1" value="1 year">
                            <label for="duration1">1 year</label>
                            <input type="radio" name="duration" id="duration2" value="2 years">
                            <label for="duration2">2 years</label>
                        </div>
                    </div>
                    <div class="btn-group">
                        <button class="btn btn-primary" onclick="addMembership()">Confirm</button>
                        <button class="btn btn-secondary" onclick="clearMaintenance()">Cancel</button>
                    </div>
                </div>
            `;
        }

        function addMembership() {
            const name = document.getElementById('memName')?.value;
            const address = document.getElementById('memAddress')?.value;
            const phone = document.getElementById('memPhone')?.value;
            const email = document.getElementById('memEmail')?.value;
            const duration = document.querySelector('input[name="duration"]:checked')?.value;
            const errorDiv = document.getElementById('membershipError');

            if (!name || !address || !phone || !email) {
                showError(errorDiv, 'All fields are mandatory');
                return;
            }

            const newMember = {
                id: members.length + 1,
                name,
                address,
                phone,
                email,
                membership: duration
            };
            members.push(newMember);
            showSuccess('Membership added successfully');
            clearMaintenance();
        }

        function showUpdateMembership() {
            if (currentRole !== 'admin') return;
            
            let options = members.map(m => `<option value="${m.id}">${m.name} (${m.membership})</option>`).join('');
            
            const content = document.getElementById('maintenanceContent');
            content.innerHTML = `
                <h3>Update Membership</h3>
                <div class="form-container">
                    <div class="error-message" id="updateMemError"></div>
                    <div class="form-group">
                        <label>Select Membership:</label>
                        <select id="membershipSelect" onchange="loadMembershipDetails()">
                            <option value="">Select a member</option>
                            ${options}
                        </select>
                    </div>
                    <div id="membershipDetails" style="display:none;">
                        <div class="form-group">
                            <label>Membership Number:</label>
                            <input type="text" id="memNumber" readonly>
                        </div>
                        <div class="form-group">
                            <label>Name:</label>
                            <input type="text" id="memName" readonly>
                        </div>
                        <div class="form-group">
                            <label>Current Membership:</label>
                            <input type="text" id="currentMem" readonly>
                        </div>
                        <div class="form-group">
                            <label>Extension Options:</label>
                            <div class="radio-group">
                                <input type="radio" name="extendDuration" id="extend6" value="6 months" checked>
                                <label for="extend6">Extend 6 months</label>
                                <input type="radio" name="extendDuration" id="extend1" value="1 year">
                                <label for="extend1">Extend 1 year</label>
                                <input type="radio" name="extendDuration" id="extend2" value="2 years">
                                <label for="extend2">Extend 2 years</label>
                            </div>
                        </div>
                        <div class="checkbox-group">
                            <input type="checkbox" id="cancelMembership">
                            <label for="cancelMembership">Cancel Membership</label>
                        </div>
                        <div class="btn-group">
                            <button class="btn btn-primary" onclick="updateMembership()">Update</button>
                            <button class="btn btn-secondary" onclick="clearMaintenance()">Cancel</button>
                        </div>
                    </div>
                </div>
            `;
        }

        function loadMembershipDetails() {
            const select = document.getElementById('membershipSelect');
            const memberId = parseInt(select.value);
            const member = members.find(m => m.id === memberId);
            
            if (member) {
                document.getElementById('memNumber').value = member.id;
                document.getElementById('memName').value = member.name;
                document.getElementById('currentMem').value = member.membership;
                document.getElementById('membershipDetails').style.display = 'block';
            }
        }

        function updateMembership() {
            const memberId = document.getElementById('memNumber')?.value;
            const cancelCheckbox = document.getElementById('cancelMembership');
            const extension = document.querySelector('input[name="extendDuration"]:checked')?.value;
            const errorDiv = document.getElementById('updateMemError');

            if (!memberId) {
                showError(errorDiv, 'Please select a membership');
                return;
            }

            const member = members.find(m => m.id === parseInt(memberId));
            if (member) {
                if (cancelCheckbox.checked) {
                    members = members.filter(m => m.id !== parseInt(memberId));
                    showSuccess('Membership cancelled successfully');
                } else {
                    member.membership = extension;
                    showSuccess('Membership updated successfully');
                }
                clearMaintenance();
            }
        }

        function showUserManagement() {
            if (currentRole !== 'admin') return;
            
            const content = document.getElementById('maintenanceContent');
            content.innerHTML = `
                <h3>User Management</h3>
                <div class="form-container">
                    <div class="error-message" id="userError"></div>
                    <div class="radio-group">
                        <input type="radio" name="userType" id="newUser" value="new" checked>
                        <label for="newUser">New User</label>
                        <input type="radio" name="userType" id="existingUser" value="existing">
                        <label for="existingUser">Existing User</label>
                    </div>
                    <div class="form-group">
                        <label>Name:</label>
                        <input type="text" id="userName" required>
                    </div>
                    <div id="existingFields" style="display:none;">
                        <div class="form-group">
                            <label>User ID:</label>
                            <input type="text" id="userId">
                        </div>
                    </div>
                    <div class="btn-group">
                        <button class="btn btn-primary" onclick="manageUser()">Submit</button>
                        <button class="btn btn-secondary" onclick="clearMaintenance()">Cancel</button>
                    </div>
                </div>
            `;

            // Add event listeners for radio buttons
            document.querySelectorAll('input[name="userType"]').forEach(radio => {
                radio.addEventListener('change', function() {
                    document.getElementById('existingFields').style.display = 
                        this.value === 'existing' ? 'block' : 'none';
                });
            });
        }

        function manageUser() {
            const userType = document.querySelector('input[name="userType"]:checked')?.value;
            const name = document.getElementById('userName')?.value;
            const userId = document.getElementById('userId')?.value;
            const errorDiv = document.getElementById('userError');

            if (!name) {
                showError(errorDiv, 'Name is mandatory');
                return;
            }

            if (userType === 'existing' && !userId) {
                showError(errorDiv, 'User ID is required for existing users');
                return;
            }

            showSuccess(`User ${userType === 'new' ? 'created' : 'updated'} successfully`);
            clearMaintenance();
        }

        function showAddBook() {
            if (currentRole !== 'admin') return;
            
            const content = document.getElementById('maintenanceContent');
            content.innerHTML = `
                <h3>Add Book/Movie</h3>
                <div class="form-container">
                    <div class="error-message" id="bookError"></div>
                    <div class="radio-group">
                        <input type="radio" name="itemType" id="itemBook" value="book" checked>
                        <label for="itemBook">Book</label>
                        <input type="radio" name="itemType" id="itemMovie" value="movie">
                        <label for="itemMovie">Movie</label>
                    </div>
                    <div class="form-group">
                        <label>Title:</label>
                        <input type="text" id="itemTitle" required>
                    </div>
                    <div class="form-group">
                        <label>Author/Director:</label>
                        <input type="text" id="itemAuthor" required>
                    </div>
                    <div class="form-group">
                        <label>ISBN/Serial No:</label>
                        <input type="text" id="itemIsbn" required>
                    </div>
                    <div class="form-group">
                        <label>Publication Year:</label>
                        <input type="number" id="itemYear" required>
                    </div>
                    <div class="form-group">
                        <label>Category:</label>
                        <select id="itemCategory" required>
                            <option value="">Select category</option>
                            <option value="fiction">Fiction</option>
                            <option value="non-fiction">Non-Fiction</option>
                            <option value="sci-fi">Sci-Fi</option>
                            <option value="drama">Drama</option>
                        </select>
                    </div>
                    <div class="btn-group">
                        <button class="btn btn-primary" onclick="addBook()">Add Item</button>
                        <button class="btn btn-secondary" onclick="clearMaintenance()">Cancel</button>
                    </div>
                </div>
            `;
        }

        function addBook() {
            const title = document.getElementById('itemTitle')?.value;
            const author = document.getElementById('itemAuthor')?.value;
            const isbn = document.getElementById('itemIsbn')?.value;
            const year = document.getElementById('itemYear')?.value;
            const category = document.getElementById('itemCategory')?.value;
            const type = document.querySelector('input[name="itemType"]:checked')?.value;
            const errorDiv = document.getElementById('bookError');

            if (!title || !author || !isbn || !year || !category) {
                showError(errorDiv, 'All fields are mandatory');
                return;
            }

            const newBook = {
                id: books.length + 1,
                name: title,
                author: author,
                serialNo: isbn,
                year: year,
                category: category,
                type: type,
                available: true
            };
            books.push(newBook);
            showSuccess(`${type === 'book' ? 'Book' : 'Movie'} added successfully`);
            clearMaintenance();
        }

                function showUpdateBook() {
                    if (currentRole !== 'admin') return;
                    
                    let options = books.map(b => `<option value="${b.id}">${b.name} (${b.serialNo})</option>`).join('');
                    
                    const content = document.getElementById('maintenanceContent');
                    content.innerHTML = `
                        <h3>Update Book/Movie</h3>
                        <div class="form-container">
                            <div class="error-message" id="updateBookError"></div>
                            <div class="form-group">
                                <label>Select Item:</label>
                                <select id="bookSelect" onchange="loadBookDetails()">
                                    <option value="">Select an item</option>
                                    ${options}
                                </select>
                            </div>
                            <div id="bookDetails" style="display:none;">
                                <div class="form-group">
                                    <label>Title:</label>
                                    <input type="text" id="bookTitle" readonly>
                                </div>
                                <div class="form-group">
                                    <label>Author:</label>
                                    <input type="text" id="bookAuthor" readonly>
                                </div>
                                <div class="form-group">
                                    <label>Availability:</label>
                                    <div class="radio-group">
                                        <input type="radio" name="availability" id="avail" value="available" checked>
                                        <label for="avail">Available</label>
                                        <input type="radio" name="availability" id="notAvail" value="not-available">
                                        <label for="notAvail">Not Available</label>
                                    </div>
                                </div>
                                <div class="btn-group">
                                    <button class="btn btn-primary" onclick="updateBook()">Update</button>
                                    <button class="btn btn-secondary" onclick="clearMaintenance()">Cancel</button>
                                </div>
                            </div>
                        </div>
                    `;
                }
        
                function loadBookDetails() {
                    const select = document.getElementById('bookSelect');
                    const bookId = parseInt(select.value);
                    const book = books.find(b => b.id === bookId);
                    
                    if (book) {
                        document.getElementById('bookTitle').value = book.name;
                        document.getElementById('bookAuthor').value = book.author;
                        document.getElementById('bookDetails').style.display = 'block';
                    }
                }
        
                function updateBook() {
                    const bookId = document.getElementById('bookSelect')?.value;
                    const availability = document.querySelector('input[name="availability"]:checked')?.value;
                    const errorDiv = document.getElementById('updateBookError');
        
                    if (!bookId) {
                        showError(errorDiv, 'Please select a book');
                        return;
                    }
        
                    const book = books.find(b => b.id === parseInt(bookId));
                    if (book) {
                        book.available = availability === 'available';
                        showSuccess('Book updated successfully');
                        clearMaintenance();
                    }
                }
        
                function clearMaintenance() {
                    document.getElementById('maintenanceContent').innerHTML = '';
                }
        
                // Reports Functions
                function showBookAvailability() {
                    const content = document.getElementById('reportsContent');
                    const availableBooks = books.filter(b => b.available);
                    
                    let tableRows = books.map(b => `
                        <tr>
                            <td>${b.name}</td>
                            <td>${b.author}</td>
                            <td>${b.serialNo}</td>
                            <td>${b.available ? 'Available' : 'Not Available'}</td>
                        </tr>
                    `).join('');
                    
                    content.innerHTML = `
                        <h3>Book Availability Report</h3>
                        <p>Total Books: ${books.length} | Available: ${availableBooks.length} | Issued: ${books.length - availableBooks.length}</p>
                        <div class="table-container">
                            <table>
                                <tr>
                                    <th>Title</th>
                                    <th>Author</th>
                                    <th>Serial No</th>
                                    <th>Status</th>
                                </tr>
                                ${tableRows}
                            </table>
                        </div>
                    `;
                }
        
                function showIssuedBooks() {
                    const content = document.getElementById('reportsContent');
                    
                    let tableRows = issuedBooks.map(ib => `
                        <tr>
                            <td>${ib.memberName}</td>
                            <td>${ib.bookName}</td>
                            <td>${ib.issueDate}</td>
                            <td>${ib.dueDate}</td>
                        </tr>
                    `).join('');
                    
                    content.innerHTML = `
                        <h3>Issued Books Report</h3>
                        <p>Total Issued: ${issuedBooks.length}</p>
                        <div class="table-container">
                            <table>
                                <tr>
                                    <th>Member Name</th>
                                    <th>Book Name</th>
                                    <th>Issue Date</th>
                                    <th>Due Date</th>
                                </tr>
                                ${tableRows || '<tr><td colspan="4">No issued books</td></tr>'}
                            </table>
                        </div>
                    `;
                }
        
                function showOverdueBooks() {
                    const content = document.getElementById('reportsContent');
                    const today = new Date();
                    
                    const overdueBooks = issuedBooks.filter(ib => new Date(ib.dueDate) < today);
                    
                    let tableRows = overdueBooks.map(ob => `
                        <tr>
                            <td>${ob.memberName}</td>
                            <td>${ob.bookName}</td>
                            <td>${ob.dueDate}</td>
                            <td>${Math.ceil((today - new Date(ob.dueDate)) / (1000 * 60 * 60 * 24))} days</td>
                        </tr>
                    `).join('');
                    
                    content.innerHTML = `
                        <h3>Overdue Books Report</h3>
                        <p>Total Overdue: ${overdueBooks.length}</p>
                        <div class="table-container">
                            <table>
                                <tr>
                                    <th>Member Name</th>
                                    <th>Book Name</th>
                                    <th>Due Date</th>
                                    <th>Days Overdue</th>
                                </tr>
                                ${tableRows || '<tr><td colspan="4">No overdue books</td></tr>'}
                            </table>
                        </div>
                    `;
                }
        
                function showMembershipReport() {
                    const content = document.getElementById('reportsContent');
                    
                    let tableRows = members.map(m => `
                        <tr>
                            <td>${m.id}</td>
                            <td>${m.name}</td>
                            <td>${m.email}</td>
                            <td>${m.membership}</td>
                        </tr>
                    `).join('');
                    
                    content.innerHTML = `
                        <h3>Membership Report</h3>
                        <p>Total Members: ${members.length}</p>
                        <div class="table-container">
                            <table>
                                <tr>
                                    <th>ID</th>
                                    <th>Name</th>
                                    <th>Email</th>
                                    <th>Membership</th>
                                </tr>
                                ${tableRows}
                            </table>
                        </div>
                    `;
                }
        
                // Transactions Functions
                function showBookIssue() {
                    const content = document.getElementById('transactionsContent');
                    const memberOptions = members.map(m => `<option value="${m.id}">${m.name}</option>`).join('');
                    const bookOptions = books.filter(b => b.available).map(b => `<option value="${b.id}">${b.name}</option>`).join('');
                    
                    content.innerHTML = `
                        <h3>Book Issue</h3>
                        <div class="form-container">
                            <div class="error-message" id="issueError"></div>
                            <div class="form-group">
                                <label>Member:</label>
                                <select id="issueMember" required>
                                    <option value="">Select member</option>
                                    ${memberOptions}
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Book:</label>
                                <select id="issueBook" required>
                                    <option value="">Select book</option>
                                    ${bookOptions}
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Issue Date:</label>
                                <input type="date" id="issueDate" required>
                            </div>
                            <div class="form-group">
                                <label>Due Date:</label>
                                <input type="date" id="dueDate" required>
                            </div>
                            <div class="btn-group">
                                <button class="btn btn-primary" onclick="issueBook()">Issue Book</button>
                                <button class="btn btn-secondary" onclick="clearTransaction()">Cancel</button>
                            </div>
                        </div>
                    `;
                }
        
                function issueBook() {
                    const memberId = document.getElementById('issueMember')?.value;
                    const bookId = document.getElementById('issueBook')?.value;
                    const issueDate = document.getElementById('issueDate')?.value;
                    const dueDate = document.getElementById('dueDate')?.value;
                    const errorDiv = document.getElementById('issueError');
        
                    if (!memberId || !bookId || !issueDate || !dueDate) {
                        showError(errorDiv, 'All fields are mandatory');
                        return;
                    }
        
                    const member = members.find(m => m.id === parseInt(memberId));
                    const book = books.find(b => b.id === parseInt(bookId));
        
                    if (member && book) {
                        issuedBooks.push({
                            memberId: parseInt(memberId),
                            memberName: member.name,
                            bookId: parseInt(bookId),
                            bookName: book.name,
                            issueDate: issueDate,
                            dueDate: dueDate
                        });
                        book.available = false;
                        showSuccess('Book issued successfully');
                        clearTransaction();
                    }
                }
        
                function showReturnBook() {
                    const content = document.getElementById('transactionsContent');
                    const returnOptions = issuedBooks.map(ib => `<option value="${ib.bookId}">${ib.bookName} - ${ib.memberName}</option>`).join('');
                    
                    content.innerHTML = `
                        <h3>Return Book</h3>
                        <div class="form-container">
                            <div class="error-message" id="returnError"></div>
                            <div class="form-group">
                                <label>Select Issued Book:</label>
                                <select id="returnBook" required>
                                    <option value="">Select a book to return</option>
                                    ${returnOptions}
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Return Date:</label>
                                <input type="date" id="returnDate" required>
                            </div>
                            <div class="btn-group">
                                <button class="btn btn-primary" onclick="returnBook()">Return Book</button>
                                <button class="btn btn-secondary" onclick="clearTransaction()">Cancel</button>
                            </div>
                        </div>
                    `;
                }
        
                function returnBook() {
                    const bookId = document.getElementById('returnBook')?.value;
                    const returnDate = document.getElementById('returnDate')?.value;
                    const errorDiv = document.getElementById('returnError');
        
                    if (!bookId || !returnDate) {
                        showError(errorDiv, 'All fields are mandatory');
                        return;
                    }
        
                    const issuedIndex = issuedBooks.findIndex(ib => ib.bookId === parseInt(bookId));
                    if (issuedIndex !== -1) {
                        const issued = issuedBooks[issuedIndex];
                        const returnD = new Date(returnDate);
                        const dueD = new Date(issued.dueDate);
                        const daysLate = Math.max(0, Math.ceil((returnD - dueD) / (1000 * 60 * 60 * 24)));
                        
                        if (daysLate > 0) {
                            fines.push({
                                memberId: issued.memberId,
                                memberName: issued.memberName,
                                amount: daysLate * 10,
                                daysLate: daysLate,
                                reason: 'Book returned late'
                            });
                            showSuccess(`Book returned successfully. Fine: Rs.${daysLate * 10} for ${daysLate} days late`);
                        } else {
                            showSuccess('Book returned successfully. No fine');
                        }
                        
                        issuedBooks.splice(issuedIndex, 1);
                        const book = books.find(b => b.id === parseInt(bookId));
                        if (book) {
                            book.available = true;
                        }
                        clearTransaction();
                    }
                }
        
                function showPayFine() {
                    const content = document.getElementById('transactionsContent');
                    const fineOptions = fines.filter(f => f.paid !== true).map(f => `<option value="${f.memberId}">${f.memberName} - Rs.${f.amount}</option>`).join('');
                    
                    content.innerHTML = `
                        <h3>Pay Fine</h3>
                        <div class="form-container">
                            <div class="error-message" id="fineError"></div>
                            <div class="form-group">
                                <label>Select Fine:</label>
                                <select id="fineSelect" onchange="loadFineDetails()">
                                    <option value="">Select a fine to pay</option>
                                    ${fineOptions}
                                </select>
                            </div>
                            <div id="fineDetails" style="display:none;">
                                <div class="form-group">
                                    <label>Fine Amount:</label>
                                    <input type="text" id="fineAmount" readonly>
                                </div>
                                <div class="form-group">
                                    <label>Paid Amount:</label>
                                    <input type="number" id="paidAmount" required>
                                </div>
                                <div class="btn-group">
                                    <button class="btn btn-primary" onclick="payFine()">Pay</button>
                                    <button class="btn btn-secondary" onclick="clearTransaction()">Cancel</button>
                                </div>
                            </div>
                        </div>
                    `;
                }
        
                function loadFineDetails() {
                    const select = document.getElementById('fineSelect');
                    const memberId = parseInt(select.value);
                    const fine = fines.find(f => f.memberId === memberId && f.paid !== true);
                    
                    if (fine) {
                        document.getElementById('fineAmount').value = fine.amount;
                        document.getElementById('fineDetails').style.display = 'block';
                    }
                }
        
                function payFine() {
                    const memberId = document.getElementById('fineSelect')?.value;
                    const paidAmount = document.getElementById('paidAmount')?.value;
                    const errorDiv = document.getElementById('fineError');
        
                    if (!memberId || !paidAmount) {
                        showError(errorDiv, 'All fields are mandatory');
                        return;
                    }
        
                    const fineIndex = fines.findIndex(f => f.memberId === parseInt(memberId) && f.paid !== true);
                    if (fineIndex !== -1) {
                        const fine = fines[fineIndex];
                        if (parseInt(paidAmount) >= fine.amount) {
                            fine.paid = true;
                            const balance = parseInt(paidAmount) - fine.amount;
                            showSuccess(`Fine paid successfully. ${balance > 0 ? 'Balance: Rs.' + balance : 'No balance'}`);
                            clearTransaction();
                        } else {
                            showError(errorDiv, `Insufficient amount. Required: Rs.${fine.amount}`);
                        }
                    }
                }
        
                function showSearchResults() {
                    const content = document.getElementById('transactionsContent');
                    content.innerHTML = `
                        <h3>Search Books</h3>
                        <div class="form-container">
                            <div class="form-group">
                                <label>Search by Title or Author:</label>
                                <input type="text" id="searchInput" placeholder="Enter title or author name" onkeyup="performSearch()">
                            </div>
                            <div id="searchResults"></div>
                        </div>
                    `;
                }
        
                function performSearch() {
                    const searchTerm = document.getElementById('searchInput')?.value.toLowerCase();
                    const resultsDiv = document.getElementById('searchResults');
                    
                    if (!searchTerm) {
                        resultsDiv.innerHTML = '';
                        return;
                    }
        
                    const results = books.filter(b => 
                        b.name.toLowerCase().includes(searchTerm) || 
                        b.author.toLowerCase().includes(searchTerm)
                    );
        
                    let tableRows = results.map(b => `
                        <tr>
                            <td>${b.name}</td>
                            <td>${b.author}</td>
                            <td>${b.serialNo}</td>
                            <td>${b.available ? 'Available' : 'Not Available'}</td>
                        </tr>
                    `).join('');
        
                    resultsDiv.innerHTML = `
                        <div class="table-container">
                            <table>
                                <tr>
                                    <th>Title</th>
                                    <th>Author</th>
                                    <th>Serial No</th>
                                    <th>Status</th>
                                </tr>
                                ${tableRows || '<tr><td colspan="4">No results found</td></tr>'}
                            </table>
                        </div>
                    `;
                }
        
                function clearTransaction() {
                    document.getElementById('transactionsContent').innerHTML = '';
                }
            </script>
        </body>
        </html>
