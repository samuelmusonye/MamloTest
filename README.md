<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>MAMLO FOODS - QUALITY CONTROL</title>
  
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #fff5e6;
      min-height: 100vh;
    }

    .sidebar {
      background-color: #6b260a;
      color: white;
      width: 240px;
      padding: 20px;
      flex-shrink: 0;
      display: flex;
      flex-direction: column;
      transition: transform 0.3s ease;
    }

    .sidebar.collapsed {
      transform: translateX(-240px);
    }

    .sidebar-logo {
      display: block;
      width: 100%;
      max-width: 180px;
      margin: 0 auto 15px;
    }

    .sidebar a {
      color: white;
      text-decoration: none;
      margin: 12px 0;
      display: block;
      font-size: 16px;
      cursor: pointer;
      padding: 8px;
      border-radius: 6px;
      transition: background-color 0.2s;
    }

    .sidebar a:hover {
      background-color: rgba(255, 255, 255, 0.15);
    }

    .sidebar a.active {
      font-weight: bold;
      background-color: rgba(255, 255, 255, 0.2);
    }

    .main {
      flex-grow: 1;
      display: flex;
      flex-direction: column;
      overflow-y: auto;
    }

    .navbar {
      background-color: #ffffff;
      padding: 15px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #e0e0e0;
      position: sticky;
      top: 0;
      z-index: 100;
    }

    .navbar .brand {
      font-size: 22px;
      font-weight: bold;
      color: #6b260a;
    }

    .navbar .actions {
      display: flex;
      align-items: center;
    }

    .navbar .actions button {
      margin-left: 12px;
      padding: 10px 18px;
      font-size: 14px;
      cursor: pointer;
      border-radius: 6px;
      border: none;
      transition: background-color 0.3s, transform 0.2s;
    }

    .navbar .actions button:hover {
      transform: translateY(-2px);
    }

    .login {
      background-color: #ff8c00;
      color: white;
    }

    .login:hover {
      background-color: #e07b00;
    }

    .signup {
      background-color: white;
      color: #6b260a;
      border: 2px solid #6b260a;
    }

    .signup:hover {
      background-color: #f5f5f5;
    }

    .hamburger {
      display: none;
      font-size: 24px;
      cursor: pointer;
      color: #6b260a;
    }

    .content {
      padding: 25px;
      overflow-y: auto;
    }

    .section {
      display: none;
    }

    .section.active {
      display: block;
    }

    .summary-box {
      background: linear-gradient(145deg, #fff0cc, #ffe6b3);
      padding: 20px;
      border-radius: 8px;
      margin-bottom: 20px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    }

    .summary-box h3 {
      color: #6b260a;
      margin-top: 0;
    }

    .summary-box ul {
      list-style: none;
      padding: 0;
    }

    .summary-box li {
      padding: 8px 0;
      border-bottom: 1px solid #f0f0f0;
    }

    fieldset {
      border: none;
      background: linear-gradient(145deg, #fff0cc, #ffe6b3);
      padding: 20px;
      margin-bottom: 25px;
      border-radius: 10px;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
    }

    fieldset legend {
      font-weight: bold;
      font-size: 18px;
      color: #6b260a;
      padding: 0 12px;
      background-color: #fff;
      border-radius: 6px;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      margin-bottom: 18px;
      position: relative;
    }

    .form-group label {
      font-weight: bold;
      color: #6b260a;
      margin-bottom: 6px;
      font-size: 14px;
    }

    .form-group label::after {
      content: '*';
      color: #ff8c00;
      margin-left: 4px;
      font-size: 12px;
    }

    .form-group input,
    .form-group select {
      width: 100%;
      max-width: 420px;
      padding: 12px;
      font-size: 14px;
      border: 1px solid #d0d0d0;
      border-radius: 6px;
      background-color: #fff;
      transition: border-color 0.3s, box-shadow 0.3s, transform 0.2s;
    }

    .form-group input:focus,
    .form-group select:focus {
      outline: none;
      border-color: #ff8c00;
      box-shadow: 0 0 6px rgba(255, 140, 0, 0.4);
      transform: scale(1.01);
    }

    .form-group input::placeholder {
      color: #aaa;
      font-style: italic;
    }

    .form-group input[list] {
      position: relative;
    }

    .form-section {
      margin-bottom: 25px;
    }

    .form-section h4 {
      color: #6b260a;
      font-size: 16px;
      margin: 15px 0 10px;
      border-bottom: 1px solid #ff8c00;
      padding-bottom: 6px;
    }

    .submit-btn {
      text-align: center;
      margin: 30px 0;
    }

    .submit-btn button {
      padding: 12px 28px;
      font-size: 16px;
      background: linear-gradient(to right, #6b260a, #8f2f0d);
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: transform 0.2s, background 0.3s;
    }

    .submit-btn button:hover {
      background: linear-gradient(to right, #8f2f0d, #6b260a);
      transform: translateY(-2px);
    }

    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }

    .modal-content {
      background-color: white;
      padding: 25px;
      border-radius: 12px;
      max-width: 420px;
      width: 90%;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
    }

    .modal-content h3 {
      text-align: center;
      color: #6b260a;
      margin-top: 0;
    }

    .modal-content label {
      display: block;
      margin: 12px 0 6px;
      font-weight: bold;
      color: #6b260a;
    }

    .modal-content input {
      width: 100%;
      padding: 12px;
      font-size: 14px;
      margin-bottom: 12px;
      border: 1px solid #d0d0d0;
      border-radius: 6px;
    }

    .modal-content button {
      width: 100%;
      padding: 12px;
      background: linear-gradient(to right, #6b260a, #8f2f0d);
      color: white;
      font-size: 16px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: background 0.3s, transform 0.2s;
    }

    .modal-content button:hover {
      background: linear-gradient(to right, #8f2f0d, #6b260a);
      transform: translateY(-2px);
    }

    .modal-content .toggle {
      margin-top: 12px;
      text-align: center;
    }

    .modal-content .toggle a {
      color: #ff8c00;
      text-decoration: none;
      font-weight: bold;
      cursor: pointer;
    }

    .modal-content .form-section {
      display: none;
    }

    .modal-content .form-section.active {
      display: block;
    }

    .otp-section {
      display: none;
    }

    .verification-section {
      display: none;
      text-align: center;
      margin-top: 20px;
    }

    .search-bar {
      margin-bottom: 20px;
    }

    .search-bar input {
      width: 100%;
      max-width: 420px;
      padding: 12px;
      font-size: 14px;
      border: 1px solid #d0d0d0;
      border-radius: 6px;
      background-color: #fff;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
      background-color: #fff;
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
    }

    th, td {
      border: 1px solid #d0d0d0;
      padding: 14px;
      text-align: left;
    }

    th {
      background: linear-gradient(to right, #6b260a, #8f2f0d);
      color: white;
      font-weight: bold;
      position: sticky;
      top: 0;
      z-index: 10;
    }

    tr:nth-child(even) {
      background-color: #fff0cc;
    }

    tr:hover {
      background-color: #ffe6b3;
    }

    .feedback {
      margin: 12px 0;
      padding: 12px;
      border-radius: 6px;
      opacity: 0;
      transition: opacity 0.5s;
    }

    .feedback.visible {
      opacity: 1;
    }

    .feedback.success {
      background-color: #d4edda;
      color: #155724;
    }

    .feedback.error {
      background-color: #f8d7da;
      color: #721c24;
    }

    .loading {
      display: none;
      text-align: center;
      margin: 12px 0;
      color: #6b260a;
      font-style: italic;
    }

    .download-btn {
      padding: 12px 24px;
      background: linear-gradient(to right, #ff8c00, #e07b00);
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      margin-top: 12px;
      transition: background 0.3s, transform 0.2s;
    }

    .download-btn:hover {
      background: linear-gradient(to right, #e07b00, #ff8c00);
      transform: translateY(-2px);
    }

    .dashboard-container {
      display: flex;
      height: 100vh;
      overflow: hidden;
      background-color: #fafafa;
    }

    @media (max-width: 768px) {
      .sidebar {
        position: fixed;
        z-index: 200;
        height: 100%;
      }

      .hamburger {
        display: block;
      }

      .main {
        margin-left: 0;
      }

      .navbar {
        flex-direction: row;
        justify-content: space-between;
      }

      .navbar .actions {
        margin-top: 0;
      }

      .content {
        padding: 15px;
      }

      .form-group {
        max-width: 100%;
      }

      .form-group input,
      .form-group select {
        max-width: 100%;
      }

      table {
        font-size: 14px;
      }

      th, td {
        padding: 10px;
      }
    }
  </style>
</head>
<body>

  <div id="authModal" class="modal">
    <div class="modal-content">
      <div id="loginSection" class="form-section active">
        <h3>Login</h3>
        <form id="authForm" onsubmit="handleAuthSubmit(); return false;">
          <div class="form-group">
            <label>Email or Phone:</label>
            <input type="text" id="loginUser" placeholder="Enter your email or phone number" required>
          </div>
          <button type="button" onclick="sendCode()">Send Code</button>
          <div id="otpSection" class="otp-section">
            <div class="form-group">
              <label>Enter OTP Code:</label>
              <input type="text" id="loginCode" placeholder="123456" required>
            </div>
            <button type="submit">Login</button>
          </div>
          <div id="authFeedback" class="feedback"></div>
        </form>
        <div class="toggle">
          Don't have an account? <a onclick="showSignUpMode()">Sign Up</a>
        </div>
      </div>

      <div id="signupSection" class="form-section">
        <h3>Sign Up</h3>
        <form id="authForm" onsubmit="handleAuthSubmit(); return false;">
          <div class="form-group">
            <label>Full Name:</label>
            <input type="text" id="signupName" placeholder="Enter your full name" required>
          </div>
          <div class="form-group">
            <label>Email:</label>
            <input type="email" id="signupEmail" placeholder="Enter your email" required>
          </div>
          <div class="form-group">
            <label>Password:</label>
            <input type="password" id="signupPass" placeholder="At least 6 characters" minlength="6" required>
          </div>
          <button type="submit">Sign Up</button>
          <div id="verificationSection" class="verification-section">
            <p>A verification link has been sent to your email. Please check your inbox.</p>
            <button type="button" onclick="confirmVerification()">Confirm Verification</button>
          </div>
          <div id="authFeedback" class="feedback"></div>
        </form>
        <div class="toggle">
          Already have an account? <a onclick="showLoginMode()">Login</a>
        </div>
      </div>
    </div>
  </div>

  <div id="dashboard" class="dashboard-container">
    <div class="sidebar">
      <img src="logo.webp" alt="Mamlo Foods Logo" class="sidebar-logo">
      <a id="navDashboard" class="active" onclick="showSection('dashboardSection')">Dashboard</a>
      <a id="navRawMaterials" onclick="showSection('rawMaterialsSection')">Raw Materials</a>
      <a id="navProcessing" onclick="showSection('processingSection')">Processing</a>
      <a id="navPackaging" onclick="showSection('packagingSection')">Packaging</a>
      <a id="navReports" onclick="showSection('reportsSection')">Reports</a>
      <a onclick="logout()">Logout</a>
    </div>

    <div class="main">
      <div class="navbar">
        <div class="brand">QUALITY CONTROL</div>
        <div class="hamburger" onclick="toggleSidebar()">☰</div>
        <div class="actions">
          <button class="login" onclick="showLoginModeFromNavbar()">Login</button>
          <button class="signup" onclick="showSignUpModeFromNavbar()">Sign Up</button>
        </div>
      </div>

      <div class="content">
        <div id="dashboardSection" class="section active">
          <h2>Welcome, <span id="userNameDisplay"></span>!</h2>
          <div class="summary-box">
            <h3>Summary</h3>
            <p>Total Raw Materials: <span id="rawMaterialsCount">0</span></p>
            <p>Total Processing: <span id="processingCount">0</span></p>
            <p>Total Packaging: <span id="packagingCount">0</span></p>
            <p>Total Reports: <span id="reportsCount">0</span></p>
          </div>
          <div class="summary-box">
            <h3>Recent Submissions</h3>
            <h4>Raw Materials</h4>
            <ul id="recentRawMaterials"></ul>
            <h4>Processing</h4>
            <ul id="recentProcessing"></ul>
            <h4>Packaging</h4>
            <ul id="recentPackaging"></ul>
            <h4>Reports</h4>
            <ul id="recentReports"></ul>
          </div>
        </div>

        <div id="rawMaterialsSection" class="section">
          <h2>Raw Materials</h2>
          <div class="search-bar">
            <input type="text" id="rawMaterialsSearch" placeholder="Search by Batch No or Supplier" oninput="debouncedFilter('rawMaterials')">
          </div>
          <div id="rawMaterialsFeedback" class="feedback"></div>
          <div id="rawMaterialsLoading" class="loading">Loading...</div>
          <form onsubmit="submitRawMaterials(event); return validateForm();">
            <fieldset>
              <legend>1.0 Raw Material</legend>
              <div class="form-section">
                <h4>Basic Information</h4>
                <div class="form-group">
                  <label>Batch No:</label>
                  <input type="text" placeholder="e.g., BATCH2025-001" list="batchNoList" required>
                  <datalist id="batchNoList"></datalist>
                </div>
                <div class="form-group">
                  <label>Origin (Supplier Name):</label>
                  <input type="text" placeholder="e.g., ABC Farms" list="supplierList" required>
                  <datalist id="supplierList"></datalist>
                </div>
                <div class="form-group">
                  <label>Peanuts Variety:</label>
                  <input type="text" placeholder="e.g., Virginia" list="varietyList" required>
                  <datalist id="varietyList"></datalist>
                </div>
              </div>
              <div class="form-section">
                <h4>1.2 Quality Inspection</h4>
                <div class="form-group">
                  <label>Physical Appearance:</label>
                  <input type="text" placeholder="e.g., Clean, no damage" required>
                </div>
                <div class="form-group">
                  <label>Color:</label>
                  <input type="text" placeholder="e.g., Light brown" required>
                </div>
                <div class="form-group">
                  <label>Foreign Matter:</label>
                  <input type="text" placeholder="e.g., None" required>
                </div>
                <div class="form-group">
                  <label>Kernel Uniformity:</label>
                  <input type="text" placeholder="e.g., Consistent" required>
                </div>
                <div class="form-group">
                  <label>Moisture Content (%):</label>
                  <input type="number" min="0" max="100" step="0.01" placeholder="e.g., 5.5" required>
                </div>
              </div>
            </fieldset>
            <div class="submit-btn">
              <button type="submit">Submit</button>
            </div>
          </form>
          <table>
            <thead>
              <tr>
                <th>Batch No</th>
                <th>Supplier</th>
                <th>Variety</th>
                <th>Appearance</th>
                <th>Color</th>
                <th>Foreign Matter</th>
                <th>Uniformity</th>
                <th>Moisture (%)</th>
              </tr>
            </thead>
            <tbody id="rawMaterialsTable"></tbody>
          </table>
        </div>

        <div id="processingSection" class="section">
          <h2>Processing</h2>
          <div class="search-bar">
            <input type="text" id="processingSearch" placeholder="Search by Batch No" oninput="debouncedFilter('processing')">
          </div>
          <div id="processingFeedback" class="feedback"></div>
          <div id="processingLoading" class="loading">Loading...</div>
          <form onsubmit="submitProcessing(event); return validateForm();">
            <fieldset>
              <legend>2.0 Processing</legend>
              <div class="form-section">
                <div class="form-group">
                  <label>Batch No:</label>
                  <input type="text" placeholder="e.g., BATCH2025-001" list="batchNoList" required>
                </div>
                <div class="form-group">
                  <label>Roasted Quantity (kg):</label>
                  <input type="number" step="0.01" placeholder="e.g., 100.50" required>
                </div>
                <div class="form-group">
                  <label>Moisture Content (%):</label>
                  <input type="number" min="0" max="100" step="0.01" placeholder="e.g., 4.0" required>
                </div>
                <div class="form-group">
                  <label>Temperature:</label>
                  <input type="text" placeholder="e.g., 150°C" required>
                </div>
                <div class="form-group">
                  <label>Time:</label>
                  <input type="text" placeholder="e.g., 30 min" required>
                </div>
              </div>
            </fieldset>
            <div class="submit-btn">
              <button type="submit">Submit</button>
            </div>
          </form>
          <table>
            <thead>
              <tr>
                <th>Batch No</th>
                <th>Roasted Qty (kg)</th>
                <th>Moisture (%)</th>
                <th>Temperature</th>
                <th>Time</th>
              </tr>
            </thead>
            <tbody id="processingTable"></tbody>
          </table>
        </div>

        <div id="packagingSection" class="section">
          <h2>Packaging</h2>
          <div class="search-bar">
            <input type="text" id="packagingSearch" placeholder="Search by Batch No or Material" oninput="debouncedFilter('packaging')">
          </div>
          <div id="packagingFeedback" class="feedback"></div>
          <div id="packagingLoading" class="loading">Loading...</div>
          <form onsubmit="submitPackaging(event); return validateForm();">
            <fieldset>
              <legend>3.0 Packaging</legend>
              <div class="form-section">
                <div class="form-group">
                  <label>Batch No:</label>
                  <input type="text" placeholder="e.g., BATCH2025-001" list="batchNoList" required>
                </div>
                <div class="form-group">
                  <label>Packaging Material:</label>
                  <input type="text" placeholder="e.g., Plastic pouch" list="materialList" required>
                  <datalist id="materialList"></datalist>
                </div>
                <div class="form-group">
                  <label>Quantity Packed (kg):</label>
                  <input type="number" step="0.01" placeholder="e.g., 50.25" required>
                </div>
                <div class="form-group">
                  <label>Seal Integrity:</label>
                  <input type="text" placeholder="e.g., Intact" required>
                </div>
                <div class="form-group">
                  <label>Label Accuracy:</label>
                  <input type="text" placeholder="e.g., Correct" required>
                </div>
              </div>
            </fieldset>
            <div class="submit-btn">
              <button type="submit">Submit</button>
            </div>
          </form>
          <table>
            <thead>
              <tr>
                <th>Batch No</th>
                <th>Material</th>
                <th>Qty Packed (kg)</th>
                <th>Seal Integrity</th>
                <th>Label Accuracy</th>
              </tr>
            </thead>
            <tbody id="packagingTable"></tbody>
          </table>
        </div>

        <div id="reportsSection" class="section">
          <h2>Reports</h2>
          <div class="search-bar">
            <input type="text" id="reportsSearch" placeholder="Search by Report Type or Summary" oninput="debouncedFilter('reports')">
          </div>
          <div id="reportsFeedback" class="feedback"></div>
          <div id="reportsLoading" class="loading">Loading...</div>
          <form onsubmit="submitReport(event); return validateForm();">
            <fieldset>
              <legend>4.0 Reports</legend>
              <div class="form-section">
                <div class="form-group">
                  <label>Report Type:</label>
                  <select required>
                    <option value="">Select Type</option>
                    <option value="daily">Daily</option>
                    <option value="weekly">Weekly</option>
                    <option value="monthly">Monthly</option>
                  </select>
                </div>
                <div class="form-group">
                  <label>Date Range:</label>
                  <input type="text" placeholder="e.g., 2025-05-01 to 2025-05-15" required>
                </div>
                <div class="form-group">
                  <label>Summary:</label>
                  <input type="text" placeholder="e.g., Quality control summary" required>
                </div>
              </div>
            </fieldset>
            <div class="submit-btn">
              <button type="submit">Generate Report</button>
            </div>
          </form>
          <table>
            <thead>
              <tr>
                <th>Report Type</th>
                <th>Date Range</th>
                <th>Summary</th>
              </tr>
            </thead>
            <tbody id="reportsTable"></tbody>
          </table>
          <button class="download-btn" onclick="downloadReport()">Download Reports CSV</button>
          <button class="download-btn" onclick="downloadAllData()">Download All Data CSVs</button>
        </div>
      </div>
    </div>
  </div>

  <script>
    let userProfile = {
      fullName: "",
      email: ""
    };

    let rawMaterialsData = [];
    let processingData = [];
    let packagingData = [];
    let reportsData = [];

    let inputHistory = {
      batchNo: new Set(),
      supplier: new Set(),
      variety: new Set(),
      material: new Set()
    };

    // Load input history from localStorage
    function loadInputHistory() {
      const savedHistory = localStorage.getItem('mamloInputHistory');
      if (savedHistory) {
        inputHistory = JSON.parse(savedHistory);
        inputHistory.batchNo = new Set(inputHistory.batchNo);
        inputHistory.supplier = new Set(inputHistory.supplier);
        inputHistory.variety = new Set(inputHistory.variety);
        inputHistory.material = new Set(inputHistory.material);
      }
      updateDatalists();
    }

    // Save input history to localStorage
    function saveInputHistory() {
      const historyToSave = {
        batchNo: Array.from(inputHistory.batchNo),
        supplier: Array.from(inputHistory.supplier),
        variety: Array.from(inputHistory.variety),
        material: Array.from(inputHistory.material)
      };
      localStorage.setItem('mamloInputHistory', JSON.stringify(historyToSave));
    }

    // Update datalists for autocomplete
    function updateDatalists() {
      const batchNoList = document.getElementById('batchNoList');
      const supplierList = document.getElementById('supplierList');
      const varietyList = document.getElementById('varietyList');
      const materialList = document.getElementById('materialList');

      batchNoList.innerHTML = Array.from(inputHistory.batchNo)
        .map(val => `<option value="${val}">`).join('');
      supplierList.innerHTML = Array.from(inputHistory.supplier)
        .map(val => `<option value="${val}">`).join('');
      varietyList.innerHTML = Array.from(inputHistory.variety)
        .map(val => `<option value="${val}">`).join('');
      materialList.innerHTML = Array.from(inputHistory.material)
        .map(val => `<option value="${val}">`).join('');
    }

    // Debounce function for search
    function debounce(func, wait) {
      let timeout;
      return function executedFunction(...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func.apply(this, args), wait);
      };
    }

    // Toggle sidebar on mobile
    function toggleSidebar() {
      const sidebar = document.querySelector('.sidebar');
      sidebar.classList.toggle('collapsed');
    }

    function showSection(sectionId) {
      document.querySelectorAll('.section').forEach(section => section.classList.remove('active'));
      document.querySelectorAll('.sidebar a').forEach(link => link.classList.remove('active'));
      document.getElementById(sectionId).classList.add('active');
      const navLinkId = `nav${sectionId.charAt(0).toUpperCase() + sectionId.slice(1).replace('Section', '')}`;
      document.getElementById(navLinkId).classList.add('active');
      if (window.innerWidth <= 768) {
        document.querySelector('.sidebar').classList.add('collapsed');
      }
      updateSummary();
    }

    function showLoginMode() {
      document.getElementById("signupSection").classList.remove("active");
      document.getElementById("loginSection").classList.add("active");
      document.getElementById("otpSection").style.display = "none";
      clearFeedback('authFeedback');
    }

    function showSignUpMode() {
      document.getElementById("loginSection").classList.remove("active");
      document.getElementById("signupSection").classList.add("active");
      document.getElementById("verificationSection").style.display = "none";
      clearFeedback('authFeedback');
    }

    function showLoginModeFromNavbar() {
      document.getElementById('authModal').style.display = 'flex';
      showLoginMode();
    }

    function showSignUpModeFromNavbar() {
      document.getElementById('authModal').style.display = 'flex';
      showSignUpMode();
    }

    function closeModal(modalId) {
      document.getElementById(modalId).style.display = 'none';
      clearFeedback('authFeedback');
    }

    function sendCode() {
      const user = document.getElementById("loginUser").value.trim();
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      const phoneRegex = /^\+?\d{10,15}$/;
      if (emailRegex.test(user) || phoneRegex.test(user)) {
        showFeedback('authFeedback', `A verification code has been sent to ${user}.`, true);
        document.getElementById("otpSection").style.display = "block";
      } else {
        showFeedback('authFeedback', 'Please enter a valid email or phone number.', false);
      }
    }

    function handleAuthSubmit() {
      const feedback = document.getElementById('authFeedback');
      const loginSection = document.getElementById("loginSection").classList.contains("active");
      if (loginSection) {
        const user = document.getElementById("loginUser").value.trim();
        const code = document.getElementById("loginCode").value.trim();
        if (!code) {
          showFeedback('authFeedback', 'Please enter the OTP code sent to your mobile/ email.', false);
          return;
        }
        userProfile.email = user;
        showFeedback('authFeedback', `Welcome back, ${user}!`, true);
        document.getElementById('userNameDisplay').innerText = user;
        setTimeout(() => closeModal('authModal'), 1000);
      } else {
        const name = document.getElementById("signupName").value.trim();
        const email = document.getElementById("signupEmail").value.trim();
        const password = document.getElementById("signupPass").value;
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!emailRegex.test(email)) {
          showFeedback('authFeedback', 'Please enter a valid email address.', false);
          return;
        }
        if (password.length < 6) {
          showFeedback('authFeedback', 'Password must be at least 6 characters.', false);
          return;
        }
        userProfile.fullName = name;
        userProfile.email = email;
        showFeedback('authFeedback', `A verification link has been sent to ${email}.`, true);
        document.getElementById("verificationSection").style.display = "block";
        document.getElementById("authForm").onsubmit = null;
      }
    }

    function confirmVerification() {
      showFeedback('authFeedback', 'Email verification confirmed.', true);
      showLoginMode();
      document.getElementById("verificationSection").style.display = "none";
      document.getElementById("authForm").onsubmit = function() { handleAuthSubmit(); return false; };
    }

    function logout() {
      if (confirm("Are you sure you want to exit?")) {
        userProfile = { fullName: "", email: "" };
        document.getElementById('userNameDisplay').innerText = "";
        rawMaterialsData = [];
        processingData = [];
        packagingData = [];
        reportsData = [];
        inputHistory = { batchNo: new Set(), supplier: new Set(), variety: new Set(), material: new Set() };
        localStorage.removeItem('mamloInputHistory');
        updateDatalists();
        updateTables();
        showSection('dashboardSection');
      }
    }

    function validateForm() {
      const numbers = document.querySelectorAll('input[type="number"]');
      for (let input of numbers) {
        const val = parseFloat(input.value);
        if (isNaN(val) || val < 0 || val > 100) {
          showFeedback(`${input.closest('.section').id.replace('Section', '')}Feedback`, 
                       "Number values must be between 0 and 100.", false);
          input.focus();
          return false;
        }
      }
      return true;
    }

    function validateBatchNo(batchNo) {
      const regex = /^BATCH\d{4}-\d{3}$/;
      return regex.test(batchNo);
    }

    function showFeedback(id, message, isSuccess) {
      const feedback = document.getElementById(id);
      feedback.textContent = message;
      feedback.className = `feedback ${isSuccess ? 'success' : 'error'}`;
      feedback.style.display = 'block';
      setTimeout(() => feedback.classList.add('visible'), 10);
      setTimeout(() => {
        feedback.classList.remove('visible');
        setTimeout(() => feedback.style.display = 'none', 500);
      }, 3000);
    }

    function clearFeedback(id) {
      const feedback = document.getElementById(id);
      feedback.classList.remove('visible');
      setTimeout(() => feedback.style.display = 'none', 500);
    }

    function showLoading(id, show) {
      document.getElementById(id).style.display = show ? 'block' : 'none';
    }

    function submitRawMaterials(event) {
      event.preventDefault();
      showLoading('rawMaterialsLoading', true);
      const inputs = document.querySelectorAll('#rawMaterialsSection input');
      const batchNo = inputs[0].value.trim();
      if (!validateBatchNo(batchNo)) {
        showFeedback('rawMaterialsFeedback', 'Batch No must be in format BATCHYYYY-NNN (e.g., BATCH2025-001).', false);
        showLoading('rawMaterialsLoading', false);
        return;
      }
      const data = {
        batch_no: batchNo,
        supplier: inputs[1].value,
        variety: inputs[2].value,
        appearance: inputs[3].value,
        color: inputs[4].value,
        foreign_matter: inputs[5].value,
        uniformity: inputs[6].value,
        moisture: parseFloat(inputs[7].value)
      };
      rawMaterialsData.push(data);
      inputHistory.batchNo.add(data.batch_no);
      inputHistory.supplier.add(data.supplier);
      inputHistory.variety.add(data.variety);
      saveInputHistory();
      updateDatalists();
      updateRawMaterialsTable();
      updateSummary();
      showFeedback('rawMaterialsFeedback', 'Data submitted successfully!', true);
      setTimeout(() => {
        showLoading('rawMaterialsLoading', false);
        inputs.forEach(input => input.value = '');
      }, 1000);
    }

    function updateRawMaterialsTable(filter = '') {
      const tbody = document.getElementById('rawMaterialsTable');
      tbody.innerHTML = '';
      const filteredData = rawMaterialsData.filter(row =>
        row.batch_no.toLowerCase().includes(filter) ||
        row.supplier.toLowerCase().includes(filter)
      );
      filteredData.forEach(row => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${row.batch_no}</td>
          <td>${row.supplier}</td>
          <td>${row.variety}</td>
          <td>${row.appearance}</td>
          <td>${row.color}</td>
          <td>${row.foreign_matter}</td>
          <td>${row.uniformity}</td>
          <td>${row.moisture}</td>
        `;
        tbody.appendChild(tr);
      });
    }

    function submitProcessing(event) {
      event.preventDefault();
      showLoading('processingLoading', true);
      const inputs = document.querySelectorAll('#processingSection input');
      const batchNo = inputs[0].value.trim();
      if (!validateBatchNo(batchNo)) {
        showFeedback('processingFeedback', 'Batch No must be in format BATCHYYYY-NNN (e.g., BATCH2025-001).', false);
        showLoading('processingLoading', false);
        return;
      }
      const data = {
        batch_no: batchNo,
        roasted_qty: parseFloat(inputs[1].value),
        moisture: parseFloat(inputs[2].value),
        temperature: inputs[3].value,
        time: inputs[4].value
      };
      processingData.push(data);
      inputHistory.batchNo.add(data.batch_no);
      saveInputHistory();
      updateDatalists();
      updateProcessingTable();
      updateSummary();
      showFeedback('processingFeedback', 'Data submitted successfully!', true);
      setTimeout(() => {
        showLoading('processingLoading', false);
        inputs.forEach(input => input.value = '');
      }, 1000);
    }

    function updateProcessingTable(filter = '') {
      const tbody = document.getElementById('processingTable');
      tbody.innerHTML = '';
      const filteredData = processingData.filter(row =>
        row.batch_no.toLowerCase().includes(filter)
      );
      filteredData.forEach(row => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${row.batch_no}</td>
          <td>${row.roasted_qty}</td>
          <td>${row.moisture}</td>
          <td>${row.temperature}</td>
          <td>${row.time}</td>
        `;
        tbody.appendChild(tr);
      });
    }

    function submitPackaging(event) {
      event.preventDefault();
      showLoading('packagingLoading', true);
      const inputs = document.querySelectorAll('#packagingSection input');
      const batchNo = inputs[0].value.trim();
      if (!validateBatchNo(batchNo)) {
        showFeedback('packagingFeedback', 'Batch No must be in format BATCHYYYY-NNN (e.g., BATCH2025-001).', false);
        showLoading('packagingLoading', false);
        return;
      }
      const data = {
        batch_no: batchNo,
        material: inputs[1].value,
        qty_packed: parseFloat(inputs[2].value),
        seal_integrity: inputs[3].value,
        label_accuracy: inputs[4].value
      };
      packagingData.push(data);
      inputHistory.batchNo.add(data.batch_no);
      inputHistory.material.add(data.material);
      saveInputHistory();
      updateDatalists();
      updatePackagingTable();
      updateSummary();
      showFeedback('packagingFeedback', 'Data submitted successfully!', true);
      setTimeout(() => {
        showLoading('packagingLoading', false);
        inputs.forEach(input => input.value = '');
      }, 1000);
    }

    function updatePackagingTable(filter = '') {
      const tbody = document.getElementById('packagingTable');
      tbody.innerHTML = '';
      const filteredData = packagingData.filter(row =>
        row.batch_no.toLowerCase().includes(filter) ||
        row.material.toLowerCase().includes(filter)
      );
      filteredData.forEach(row => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${row.batch_no}</td>
          <td>${row.material}</td>
          <td>${row.qty_packed}</td>
          <td>${row.seal_integrity}</td>
          <td>${row.label_accuracy}</td>
        `;
        tbody.appendChild(tr);
      });
    }

    function submitReport(event) {
      event.preventDefault();
      showLoading('reportsLoading', true);
      const select = document.querySelector('#reportsSection select');
      const inputs = document.querySelectorAll('#reportsSection input');
      const data = {
        report_type: select.value,
        date_range: inputs[0].value,
        summary: inputs[1].value
      };
      reportsData.push(data);
      updateReportsTable();
      updateSummary();
      showFeedback('reportsFeedback', 'Report generated successfully!', true);
      setTimeout(() => {
        showLoading('reportsLoading', false);
        select.value = '';
        inputs.forEach(input => input.value = '');
      }, 1000);
    }

    function updateReportsTable(filter = '') {
      const tbody = document.getElementById('reportsTable');
      tbody.innerHTML = '';
      const filteredData = reportsData.filter(row =>
        row.report_type.toLowerCase().includes(filter) ||
        row.summary.toLowerCase().includes(filter)
      );
      filteredData.forEach(row => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${row.report_type}</td>
          <td>${row.date_range}</td>
          <td>${row.summary}</td>
        `;
        tbody.appendChild(tr);
      });
    }

    function filterTable(section) {
      const searchInput = document.getElementById(`${section}Search`).value.toLowerCase();
      if (section === 'rawMaterials') updateRawMaterialsTable(searchInput);
      else if (section === 'processing') updateProcessingTable(searchInput);
      else if (section === 'packaging') updatePackagingTable(searchInput);
      else if (section === 'reports') updateReportsTable(searchInput);
    }

    const debouncedFilter = debounce(filterTable, 300);

    function updateSummary() {
      document.getElementById('rawMaterialsCount').textContent = rawMaterialsData.length;
      document.getElementById('processingCount').textContent = processingData.length;
      document.getElementById('packagingCount').textContent = packagingData.length;
      document.getElementById('reportsCount').textContent = reportsData.length;

      const recentRawMaterials = document.getElementById('recentRawMaterials');
      recentRawMaterials.innerHTML = rawMaterialsData.slice(-5).map(row => 
        `<li>Batch ${row.batch_no} - ${row.supplier}</li>`
      ).join('');

      const recentProcessing = document.getElementById('recentProcessing');
      recentProcessing.innerHTML = processingData.slice(-5).map(row => 
        `<li>Batch ${row.batch_no} - ${row.roasted_qty}kg</li>`
      ).join('');

      const recentPackaging = document.getElementById('recentPackaging');
      recentPackaging.innerHTML = packagingData.slice(-5).map(row => 
        `<li>Batch ${row.batch_no} - ${row.material}</li>`
      ).join('');

      const recentReports = document.getElementById('recentReports');
      recentReports.innerHTML = reportsData.slice(-5).map(row => 
        `<li>${row.report_type} - ${row.date_range}</li>`
      ).join('');
    }

    function downloadReport() {
      try {
        const csvContent = [
          ['Report Type', 'Date Range', 'Summary'],
          ...reportsData.map(row => [row.report_type, row.date_range, row.summary])
        ].map(row => row.join(',')).join('\n');
        const blob = new Blob([csvContent], { type: 'text/csv' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = 'mamlo_reports.csv';
        a.click();
        URL.revokeObjectURL(url);
        showFeedback('reportsFeedback', 'Report downloaded successfully!', true);
      } catch (error) {
        showFeedback('reportsFeedback', 'Failed to download report.', false);
      }
    }

    function downloadAllData() {
      try {
        const sections = [
          {
            name: 'raw_materials',
            data: rawMaterialsData,
            headers: ['Batch No', 'Supplier', 'Variety', 'Appearance', 'Color', 'Foreign Matter', 'Uniformity', 'Moisture (%)']
          },
          {
            name: 'processing',
            data: processingData,
            headers: ['Batch No', 'Roasted Qty (kg)', 'Moisture (%)', 'Temperature', 'Time']
          },
          {
            name: 'packaging',
            data: packagingData,
            headers: ['Batch No', 'Material', 'Qty Packed (kg)', 'Seal Integrity', 'Label Accuracy']
          },
          {
            name: 'reports',
            data: reportsData,
            headers: ['Report Type', 'Date Range', 'Summary']
          }
        ];

        sections.forEach(section => {
          const csvContent = [
            section.headers,
            ...section.data.map(row => section.headers.map(h => 
              row[h.toLowerCase().replace(/ /g, '_').replace('_(%)', '')] || ''
            ))
          ].map(row => row.join(',')).join('\n');
          const blob = new Blob([csvContent], { type: 'text/csv' });
          const url = URL.createObjectURL(blob);
          const a = document.createElement('a');
          a.href = url;
          a.download = `mamlo_${section.name}.csv`;
          a.click();
          URL.revokeObjectURL(url);
        });
        showFeedback('reportsFeedback', 'All data downloaded successfully!', true);
      } catch (error) {
        showFeedback('reportsFeedback', 'Failed to download all data.', false);
      }
    }

    function updateTables() {
      updateRawMaterialsTable();
      updateProcessingTable();
      updatePackagingTable();
      updateReportsTable();
      updateSummary();
    }

    window.onclick = function(event) {
      const authModal = document.getElementById('authModal');
      if (event.target === authModal) closeModal('authModal');
    };

    // Initialize
    loadInputHistory();
    updateTables();
    updateSummary();
  </script>
</body>
</html>
