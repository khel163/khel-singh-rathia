<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>ग्राम समिति - खेल सिंह रजिस्टर</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Inter', 'Noto Sans Devanagari', sans-serif; background: #eef2f5; color: #1e2a3e; overflow-x: hidden; }
        .sidebar { position: fixed; top: 0; left: -280px; width: 280px; height: 100%; background: linear-gradient(180deg, #0b3b3a 0%, #1b5e4d 100%); color: white; z-index: 1000; transition: left 0.3s ease; box-shadow: 4px 0 20px rgba(0,0,0,0.2); padding: 1.5rem 1rem; overflow-y: auto; }
        .sidebar.open { left: 0; }
        .sidebar-header { font-size: 1.5rem; font-weight: bold; text-align: center; padding-bottom: 1.5rem; border-bottom: 1px solid rgba(255,255,255,0.2); margin-bottom: 1.5rem; display: flex; align-items: center; gap: 12px; justify-content: center; }
        .nav-item { display: flex; align-items: center; gap: 14px; padding: 12px 16px; margin: 8px 0; border-radius: 28px; background: rgba(255,255,255,0.08); cursor: pointer; transition: 0.2s; font-weight: 500; }
        .nav-item:hover { background: rgba(255,255,255,0.2); transform: translateX(5px); }
        .sidebar-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; }
        .sidebar-overlay.active { display: block; }
        .top-bar { background: #ffffffcc; backdrop-filter: blur(12px); padding: 12px 24px; display: flex; align-items: center; gap: 20px; position: sticky; top: 0; z-index: 100; border-bottom: 1px solid #dce3ec; }
        .menu-btn { background: #1f6e5c; border: none; color: white; font-size: 1.4rem; width: 44px; height: 44px; border-radius: 30px; cursor: pointer; }
        .app-title { font-weight: 700; font-size: 1.2rem; color: #1e3a38; }
        .container { max-width: 1200px; margin: 1.5rem auto; padding: 0 1.5rem; }
        .button-grid { display: flex; flex-wrap: wrap; gap: 1rem; margin-bottom: 2rem; justify-content: center; }
        .action-btn { background: white; border: none; padding: 1rem 1.8rem; border-radius: 60px; font-weight: 600; font-size: 1rem; display: inline-flex; align-items: center; gap: 12px; cursor: pointer; transition: all 0.2s; box-shadow: 0 4px 10px rgba(0,0,0,0.05); color: #1f5e4d; border: 1px solid #e2e8f0; }
        .action-btn i { font-size: 1.2rem; }
        .action-btn:hover { transform: translateY(-3px); box-shadow: 0 10px 20px rgba(0,0,0,0.1); border-color: #1f6e5c; background: #f8fafc; }
        .btn-primary { background: #1f6e5c; color: white; border: none; }
        .btn-primary:hover { background: #0f5444; }
        .btn-danger { background: #dc2626; color: white; border: none; }
        .btn-danger:hover { background: #b91c1c; }
        .btn-warning { background: #e67e22; color: white; border: none; }
        .btn-warning:hover { background: #d35400; }
        .btn-success { background: #27ae60; color: white; border: none; }
        .btn-success:hover { background: #1e8449; }
        .summary-panel { display: flex; flex-wrap: wrap; gap: 1rem; margin-bottom: 2rem; }
        .stat-card { background: white; border-radius: 28px; padding: 1.2rem; flex: 1; text-align: center; box-shadow: 0 4px 12px rgba(0,0,0,0.05); border: 1px solid #eef2f6; }
        .stat-value { font-size: 1.8rem; font-weight: 800; margin: 8px 0; }
        .donation-stat .stat-value { color: #2b9348; }
        .expense-stat .stat-value { color: #e85d04; }
        .balance-stat .stat-value { color: #1b5e4d; }
        .stat-card i { font-size: 1.6rem; }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); z-index: 2000; align-items: center; justify-content: center; backdrop-filter: blur(4px); }
        .modal.active { display: flex; }
        .modal-content { background: white; width: 90%; max-width: 550px; max-height: 85vh; border-radius: 32px; padding: 1.5rem; overflow-y: auto; animation: fadeInUp 0.2s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.2rem; font-size: 1.3rem; font-weight: 700; color: #1f5e4d; }
        .close-modal { background: none; font-size: 1.8rem; padding: 0; color: #6c757d; cursor: pointer; }
        .close-modal:hover { color: #dc2626; }
        .input-group { margin-bottom: 1rem; }
        .input-group label { font-size: 0.75rem; font-weight: 600; color: #2c6e5c; display: block; margin-bottom: 5px; }
        .input-group input, .search-box input { width: 100%; padding: 12px 14px; border-radius: 20px; border: 1.5px solid #e2e8f0; font-family: inherit; }
        .modal-buttons { display: flex; gap: 12px; margin-top: 1.2rem; }
        .modal-buttons button { flex: 1; justify-content: center; }
        button { font-family: inherit; background: #1f6e5c; border: none; padding: 10px 18px; border-radius: 40px; font-weight: 600; color: white; cursor: pointer; }
        .btn-outline { background: transparent; border: 1.5px solid #1f6e5c; color: #1f6e5c; }
        .search-box { margin-bottom: 1.2rem; position: relative; }
        .search-box i { position: absolute; left: 15px; top: 50%; transform: translateY(-50%); color: #94a3b8; }
        .search-box input { padding-left: 40px; }
        .list-table { width: 100%; border-collapse: collapse; font-size: 0.85rem; }
        .list-table th, .list-table td { padding: 10px 8px; text-align: center; border-bottom: 1px solid #e2e8f0; }
        .list-table th { background: #f8fafc; font-weight: 600; }
        .no-data { text-align: center; padding: 1.5rem; color: #94a3b8; }
        .action-icons { display: flex; gap: 8px; justify-content: center; }
        .edit-icon, .delete-icon { cursor: pointer; padding: 5px 8px; border-radius: 20px; font-size: 0.75rem; display: inline-flex; align-items: center; gap: 4px; }
        .edit-icon { background: #eef2ff; color: #2563eb; }
        .delete-icon { background: #fee2e2; color: #dc2626; }
        .edit-icon:hover { background: #e0e7ff; }
        .delete-icon:hover { background: #fecaca; }
        .password-input { width: 100%; padding: 12px 14px; border-radius: 20px; border: 1.5px solid #e2e8f0; font-family: inherit; font-size: 1rem; }
        footer { text-align: center; font-size: 0.7rem; padding: 1rem; color: #6c757d; }
        @media (max-width: 680px) { .button-grid { flex-direction: column; } .action-btn { justify-content: center; } .stat-value { font-size: 1.3rem; } }
        .toast-msg { position: fixed; bottom: 20px; right: 20px; background: #1f6e5c; color: white; padding: 12px 20px; border-radius: 40px; font-size: 0.8rem; z-index: 9999; animation: fadeOut 3s ease forwards; }
        @keyframes fadeOut { 0% { opacity: 1; } 70% { opacity: 1; } 100% { opacity: 0; visibility: hidden; } }
    </style>
</head>
<body>
    <div class="sidebar" id="sidebar">
        <div class="sidebar-header"><i class="fas fa-tree"></i> <span>ग्राम समिति</span></div>
        <div class="nav-item" id="navBackupRestore"><i class="fas fa-database"></i> <span>बैकअप / रिस्टोर</span></div>
        <div class="nav-item" id="navExportImport"><i class="fas fa-file-excel"></i> <span>एक्सेल/CSV</span></div>
        <div class="nav-item" id="navPrintReport"><i class="fas fa-print"></i> <span>प्रिंट रिपोर्ट</span></div>
        <div class="nav-item" id="navChangePassword"><i class="fas fa-key"></i> <span>पासवर्ड बदलें 🔐</span></div>
        <div class="nav-item" id="navDeleteAll"><i class="fas fa-trash-alt"></i> <span>सारा डेटा डिलीट</span></div>
    </div>
    <div class="sidebar-overlay" id="sidebarOverlay"></div>

    <div class="top-bar">
        <button class="menu-btn" id="menuToggle"><i class="fas fa-bars"></i></button>
        <div class="app-title"><i class="fas fa-hand-holding-usd"></i> खेल सिंह - ग्राम समिति रजिस्टर</div>
    </div>

    <div class="container">
        <div class="summary-panel">
            <div class="stat-card donation-stat"><i class="fas fa-donate"></i><div class="stat-label">कुल चंदा</div><div class="stat-value" id="totalDonationDisplay">₹0</div></div>
            <div class="stat-card expense-stat"><i class="fas fa-chart-line"></i><div class="stat-label">कुल खर्च</div><div class="stat-value" id="totalExpenseDisplay">₹0</div></div>
            <div class="stat-card balance-stat"><i class="fas fa-piggy-bank"></i><div class="stat-label">शेष राशि</div><div class="stat-value" id="balanceDisplay">₹0</div></div>
        </div>

        <div class="button-grid">
            <button class="action-btn btn-primary" id="addDonationBtn"><i class="fas fa-plus-circle"></i> चंदा जोड़ें</button>
            <button class="action-btn btn-primary" id="addExpenseBtn"><i class="fas fa-minus-circle"></i> खर्च जोड़ें</button>
            <button class="action-btn" id="viewDonationBtn"><i class="fas fa-list-ul"></i> चंदा विवरण 🔍</button>
            <button class="action-btn" id="viewExpenseBtn"><i class="fas fa-receipt"></i> खर्च विवरण 🔍</button>
        </div>

        <div class="button-grid" id="backupCard" style="margin-top: 0; border-top: 1px solid #e2e8f0; padding-top: 1rem;">
            <button id="backupBtn" class="action-btn"><i class="fas fa-download"></i> बैकअप (JSON)</button>
            <label for="restoreFileInput" class="action-btn btn-success" style="cursor:pointer;"><i class="fas fa-upload"></i> रिस्टोर (मर्ज करें)</label>
            <input type="file" id="restoreFileInput" accept=".json" style="display:none;">
            <button id="exportDonationCSVBtn" class="action-btn"><i class="fas fa-file-csv"></i> चंदा CSV</button>
            <button id="exportExpenseCSVBtn" class="action-btn"><i class="fas fa-file-csv"></i> खर्च CSV</button>
            <button id="exportExcelBtn" class="action-btn"><i class="fas fa-file-excel"></i> Excel</button>
            <button id="printReportBtn" class="action-btn"><i class="fas fa-print"></i> प्रिंट</button>
            <button id="changePasswordBtn" class="action-btn btn-warning"><i class="fas fa-key"></i> पासवर्ड बदलें</button>
            <button id="deleteAllDataBtn" class="action-btn btn-danger"><i class="fas fa-trash-alt"></i> 🗑️ सारा डेटा डिलीट</button>
        </div>
    </div>
    <footer>© 2025 खेल सिंह | ✏️ एडिट | 🗑️ डिलीट | 🔐 पासवर्ड से सुरक्षित | ✅ रिस्टोर में पुराना डेटा रहेगा + नया मर्ज होगा (डुप्लीकेट नहीं)</footer>

    <!-- MODALS -->
    <div id="donationModal" class="modal"><div class="modal-content"><div class="modal-header"><span><i class="fas fa-hand-holding-heart"></i> नया चंदा</span><span class="close-modal" id="closeDonationModal">&times;</span></div>
    <div class="input-group"><label>देनदार का नाम</label><input type="text" id="modalDonationName" placeholder="जैसे: रामप्रसाद"></div>
    <div class="input-group"><label>देनदार के गाँव का नाम</label><input type="text" id="modalDonationVillage" placeholder="जैसे: धनपुरी"></div>
    <div class="input-group"><label>राशि (₹)</label><input type="number" id="modalDonationAmount" step="any" placeholder="0"></div>
    <div class="input-group"><label>तारीख</label><input type="date" id="modalDonationDate"></div>
    <div class="modal-buttons"><button id="saveDonationModalBtn"><i class="fas fa-save"></i> जोड़ें</button><button id="cancelDonationModalBtn" class="btn-outline">रद्द</button></div></div></div>

    <div id="expenseModal" class="modal"><div class="modal-content"><div class="modal-header"><span><i class="fas fa-receipt"></i> नया खर्च</span><span class="close-modal" id="closeExpenseModal">&times;</span></div>
    <div class="input-group"><label>खर्च का नाम</label><input type="text" id="modalExpenseName" placeholder="जैसे: मरम्मत, भोज"></div>
    <div class="input-group"><label>राशि (₹)</label><input type="number" id="modalExpenseAmount" step="any" placeholder="0"></div>
    <div class="input-group"><label>तारीख</label><input type="date" id="modalExpenseDate"></div>
    <div class="modal-buttons"><button id="saveExpenseModalBtn"><i class="fas fa-save"></i> जोड़ें</button><button id="cancelExpenseModalBtn" class="btn-outline">रद्द</button></div></div></div>

    <div id="donationListModal" class="modal"><div class="modal-content" style="max-width: 750px;"><div class="modal-header"><span><i class="fas fa-list-ul"></i> चंदा विवरण</span><span class="close-modal" id="closeDonationListModal">&times;</span></div>
    <div class="search-box"><i class="fas fa-search"></i><input type="text" id="donationSearchInput" placeholder="नाम या गाँव से खोजें..."></div>
    <div style="overflow-x: auto; max-height: 55vh;"><table class="list-table" id="donationListTable"><thead><tr><th>क्र.सं.</th><th>नाम</th><th>गाँव</th><th>राशि (₹)</th><th>तारीख</th><th>क्रियाएं</th></tr></thead><tbody id="donationListBody"></tbody></table></div>
    <div class="modal-buttons"><button id="closeDonationListBtn" class="btn-outline">बंद करें</button></div></div></div>

    <div id="expenseListModal" class="modal"><div class="modal-content" style="max-width: 750px;"><div class="modal-header"><span><i class="fas fa-receipt"></i> खर्च विवरण</span><span class="close-modal" id="closeExpenseListModal">&times;</span></div>
    <div class="search-box"><i class="fas fa-search"></i><input type="text" id="expenseSearchInput" placeholder="नाम से खोजें..."></div>
    <div style="overflow-x: auto; max-height: 55vh;"><table class="list-table" id="expenseListTable"><thead><tr><th>क्र.सं.</th><th>खर्च का नाम</th><th>राशि (₹)</th><th>तारीख</th><th>क्रियाएं</th></tr></thead><tbody id="expenseListBody"></tbody></table></div>
    <div class="modal-buttons"><button id="closeExpenseListBtn" class="btn-outline">बंद करें</button></div></div></div>

    <div id="editDonationModal" class="modal"><div class="modal-content"><div class="modal-header"><span><i class="fas fa-edit"></i> चंदा संपादित करें</span><span class="close-modal" id="closeEditDonationModal">&times;</span></div>
    <div class="input-group"><label>देनदार का नाम</label><input type="text" id="editDonationName"></div>
    <div class="input-group"><label>देनदार का गाँव</label><input type="text" id="editDonationVillage"></div>
    <div class="input-group"><label>राशि (₹)</label><input type="number" id="editDonationAmount" step="any"></div>
    <div class="input-group"><label>तारीख</label><input type="date" id="editDonationDate"></div>
    <div class="modal-buttons"><button id="saveEditDonationBtn"><i class="fas fa-save"></i> सुरक्षित करें</button><button id="cancelEditDonationBtn" class="btn-outline">रद्द</button></div></div></div>

    <div id="editExpenseModal" class="modal"><div class="modal-content"><div class="modal-header"><span><i class="fas fa-edit"></i> खर्च संपादित करें</span><span class="close-modal" id="closeEditExpenseModal">&times;</span></div>
    <div class="input-group"><label>खर्च का नाम</label><input type="text" id="editExpenseName"></div>
    <div class="input-group"><label>राशि (₹)</label><input type="number" id="editExpenseAmount" step="any"></div>
    <div class="input-group"><label>तारीख</label><input type="date" id="editExpenseDate"></div>
    <div class="modal-buttons"><button id="saveEditExpenseBtn"><i class="fas fa-save"></i> सुरक्षित करें</button><button id="cancelEditExpenseBtn" class="btn-outline">रद्द</button></div></div></div>

    <div id="changePasswordModal" class="modal"><div class="modal-content"><div class="modal-header"><span><i class="fas fa-key"></i> पासवर्ड बदलें</span><span class="close-modal" id="closeChangePasswordModal">&times;</span></div>
    <div class="input-group"><label>पुराना पासवर्ड</label><input type="password" id="oldPasswordInput" class="password-input" placeholder="पुराना पासवर्ड दर्ज करें"></div>
    <div class="input-group"><label>नया पासवर्ड</label><input type="password" id="newPasswordInput" class="password-input" placeholder="नया पासवर्ड दर्ज करें (कम से कम 4 अक्षर)"></div>
    <div class="input-group"><label>नया पासवर्ड दोबारा</label><input type="password" id="confirmNewPasswordInput" class="password-input" placeholder="नया पासवर्ड दोबारा दर्ज करें"></div>
    <div class="modal-buttons"><button id="savePasswordBtn"><i class="fas fa-save"></i> पासवर्ड बदलें</button><button id="cancelPasswordBtn" class="btn-outline">रद्द</button></div></div></div>

    <div id="passwordModal" class="modal"><div class="modal-content"><div class="modal-header"><span><i class="fas fa-lock"></i> पासवर्ड कन्फर्मेशन</span><span class="close-modal" id="closePasswordModal">&times;</span></div>
    <div class="input-group"><label>सारा डेटा डिलीट करने के लिए पासवर्ड दर्ज करें</label><input type="password" id="deletePasswordInput" class="password-input" placeholder="पासवर्ड दर्ज करें"></div>
    <div class="modal-buttons"><button id="confirmDeleteBtn" class="btn-danger"><i class="fas fa-trash-alt"></i> डिलीट करें</button><button id="cancelDeleteBtn" class="btn-outline">रद्द</button></div></div></div>

    <script src="https://cdn.sheetjs.com/xlsx-0.20.2/package/dist/xlsx.full.min.js"></script>
    <script>
        // ---------- DATA ----------
        let donations = [];
        let expenses = [];
        let totalDonation = 0, totalExpense = 0;
        const STORAGE_DONATIONS = 'gram_donations_v5';
        const STORAGE_EXPENSES = 'gram_expenses_v5';
        const STORAGE_PASSWORD = 'gram_password';
        const DEFAULT_PASSWORD = 'admin123';

        function getCurrentPassword() { return localStorage.getItem(STORAGE_PASSWORD) || DEFAULT_PASSWORD; }
        function setNewPassword(newPassword) { localStorage.setItem(STORAGE_PASSWORD, newPassword); }

        let currentEditDonationId = null, currentEditExpenseId = null;

        const totalDonSpan = document.getElementById('totalDonationDisplay');
        const totalExpSpan = document.getElementById('totalExpenseDisplay');
        const balanceSpan = document.getElementById('balanceDisplay');

        function showToast(message) {
            const toast = document.createElement('div');
            toast.className = 'toast-msg';
            toast.innerHTML = message;
            document.body.appendChild(toast);
            setTimeout(() => toast.remove(), 3000);
        }

        function recalcTotals() {
            totalDonation = donations.reduce((s, d) => s + (d.amount || 0), 0);
            totalExpense = expenses.reduce((s, e) => s + (e.amount || 0), 0);
            totalDonSpan.innerHTML = `₹${totalDonation.toFixed(2)}`;
            totalExpSpan.innerHTML = `₹${totalExpense.toFixed(2)}`;
            balanceSpan.innerHTML = `₹${(totalDonation - totalExpense).toFixed(2)}`;
        }

        function persist() {
            localStorage.setItem(STORAGE_DONATIONS, JSON.stringify(donations));
            localStorage.setItem(STORAGE_EXPENSES, JSON.stringify(expenses));
        }

        function loadData() {
            const storedDon = localStorage.getItem(STORAGE_DONATIONS);
            const storedExp = localStorage.getItem(STORAGE_EXPENSES);
            donations = storedDon ? JSON.parse(storedDon) : [];
            expenses = storedExp ? JSON.parse(storedExp) : [];
            donations = donations.filter(d => d && typeof d.amount === 'number').map(d => ({ ...d, amount: Number(d.amount), village: d.village || '' }));
            expenses = expenses.filter(e => e && typeof e.amount === 'number').map(e => ({ ...e, amount: Number(e.amount) }));
            recalcTotals();
            refreshListModals();
        }

        function refreshListModals() { renderDonationList(); renderExpenseList(); }

        function renderDonationList(searchTerm = '') {
            const tbody = document.getElementById('donationListBody');
            if (!tbody) return;
            let filtered = [...donations];
            if (searchTerm) filtered = filtered.filter(d => d.name.toLowerCase().includes(searchTerm.toLowerCase()) || (d.village||'').toLowerCase().includes(searchTerm.toLowerCase()));
            if (filtered.length === 0) { tbody.innerHTML = '<tr><td colspan="6" class="no-data">कोई चंदा नहीं मिला</td></tr>'; return; }
            tbody.innerHTML = filtered.map((d, idx) => `<tr><td style="text-align:center">${idx+1}</td><td style="text-align:center">${escapeHtml(d.name)}</td><td style="text-align:center">${escapeHtml(d.village||'-')}</td><td style="text-align:center">₹${d.amount.toFixed(2)}</td><td style="text-align:center">${d.date}</td><td style="text-align:center"><div class="action-icons"><span class="edit-icon" onclick="editDonation('${d.id}')"><i class="fas fa-edit"></i> संपादन</span><span class="delete-icon" onclick="deleteDonation('${d.id}')"><i class="fas fa-trash-alt"></i> हटाएँ</span></div></td></tr>`).join('');
        }

        function renderExpenseList(searchTerm = '') {
            const tbody = document.getElementById('expenseListBody');
            if (!tbody) return;
            let filtered = [...expenses];
            if (searchTerm) filtered = filtered.filter(e => e.name.toLowerCase().includes(searchTerm.toLowerCase()));
            if (filtered.length === 0) { tbody.innerHTML = '<tr><td colspan="5" class="no-data">कोई खर्च नहीं मिला</td></tr>'; return; }
            tbody.innerHTML = filtered.map((e, idx) => `<tr><td style="text-align:center">${idx+1}</td><td style="text-align:center">${escapeHtml(e.name)}</td><td style="text-align:center">₹${e.amount.toFixed(2)}</td><td style="text-align:center">${e.date}</td><td style="text-align:center"><div class="action-icons"><span class="edit-icon" onclick="editExpense('${e.id}')"><i class="fas fa-edit"></i> संपादन</span><span class="delete-icon" onclick="deleteExpense('${e.id}')"><i class="fas fa-trash-alt"></i> हटाएँ</span></div></td></tr>`).join('');
        }

        window.editDonation = function(id) {
            const donation = donations.find(d => d.id == id);
            if (donation) {
                currentEditDonationId = id;
                document.getElementById('editDonationName').value = donation.name;
                document.getElementById('editDonationVillage').value = donation.village || '';
                document.getElementById('editDonationAmount').value = donation.amount;
                document.getElementById('editDonationDate').value = donation.date;
                document.getElementById('editDonationModal').classList.add('active');
            }
        }

        window.editExpense = function(id) {
            const expense = expenses.find(e => e.id == id);
            if (expense) {
                currentEditExpenseId = id;
                document.getElementById('editExpenseName').value = expense.name;
                document.getElementById('editExpenseAmount').value = expense.amount;
                document.getElementById('editExpenseDate').value = expense.date;
                document.getElementById('editExpenseModal').classList.add('active');
            }
        }

        function saveEditDonation() {
            const newName = document.getElementById('editDonationName').value.trim();
            const newVillage = document.getElementById('editDonationVillage').value.trim();
            const newAmount = parseFloat(document.getElementById('editDonationAmount').value);
            const newDate = document.getElementById('editDonationDate').value;
            if (!newName || isNaN(newAmount) || newAmount <= 0 || !newDate) { alert('कृपया सही जानकारी भरें'); return; }
            const donation = donations.find(d => d.id == currentEditDonationId);
            if (donation) { donation.name = newName; donation.village = newVillage; donation.amount = newAmount; donation.date = newDate; persist(); recalcTotals(); refreshListModals(); document.getElementById('editDonationModal').classList.remove('active'); showToast('✅ चंदा अपडेट हो गया!'); }
        }

        function saveEditExpense() {
            const newName = document.getElementById('editExpenseName').value.trim();
            const newAmount = parseFloat(document.getElementById('editExpenseAmount').value);
            const newDate = document.getElementById('editExpenseDate').value;
            if (!newName || isNaN(newAmount) || newAmount <= 0 || !newDate) { alert('कृपया सही जानकारी भरें'); return; }
            const expense = expenses.find(e => e.id == currentEditExpenseId);
            if (expense) { expense.name = newName; expense.amount = newAmount; expense.date = newDate; persist(); recalcTotals(); refreshListModals(); document.getElementById('editExpenseModal').classList.remove('active'); showToast('✅ खर्च अपडेट हो गया!'); }
        }

        window.deleteDonation = function(id) {
            if (confirm('क्या आप इस चंदा रिकॉर्ड को हटाना चाहते हैं?')) {
                donations = donations.filter(d => d.id != id);
                persist(); recalcTotals(); refreshListModals();
                showToast('🗑️ चंदा हटा दिया गया!');
            }
        }

        window.deleteExpense = function(id) {
            if (confirm('क्या आप इस खर्च रिकॉर्ड को हटाना चाहते हैं?')) {
                expenses = expenses.filter(e => e.id != id);
                persist(); recalcTotals(); refreshListModals();
                showToast('🗑️ खर्च हटा दिया गया!');
            }
        }

        function deleteAllData() {
            donations = [];
            expenses = [];
            persist();
            recalcTotals();
            refreshListModals();
            showToast('⚠️ सारा डेटा हटा दिया गया!');
        }

        function mergeRestoreData(file) {
            const reader = new FileReader();
            reader.onload = e => {
                try {
                    const parsed = JSON.parse(e.target.result);
                    let newDonations = parsed.donations || [];
                    let newExpenses = parsed.expenses || [];
                    let addedDonations = 0, addedExpenses = 0, skippedDonations = 0, skippedExpenses = 0;
                    for (const newDon of newDonations) {
                        const exists = donations.some(d => d.id === newDon.id);
                        if (!exists) { donations.push({ ...newDon, amount: Number(newDon.amount), village: newDon.village || '' }); addedDonations++; }
                        else { skippedDonations++; }
                    }
                    for (const newExp of newExpenses) {
                        const exists = expenses.some(e => e.id === newExp.id);
                        if (!exists) { expenses.push({ ...newExp, amount: Number(newExp.amount) }); addedExpenses++; }
                        else { skippedExpenses++; }
                    }
                    persist(); recalcTotals(); refreshListModals();
                    let msg = `✅ रिस्टोर पूरा!\n📥 नया जुड़ा: चंदा ${addedDonations}, खर्च ${addedExpenses}\n`;
                    if (skippedDonations > 0 || skippedExpenses > 0) msg += `⏭️ डुप्लीकेट छोड़े: चंदा ${skippedDonations}, खर्च ${skippedExpenses}`;
                    alert(msg); showToast('✅ डेटा मर्ज हो गया! पुराना डेटा सुरक्षित है');
                } catch(err) { alert('त्रुटि: फाइल पढ़ने में समस्या - ' + err.message); }
            };
            reader.readAsText(file);
        }

        function changePassword() {
            const oldPassword = document.getElementById('oldPasswordInput').value;
            const newPassword = document.getElementById('newPasswordInput').value;
            const confirmPassword = document.getElementById('confirmNewPasswordInput').value;
            const currentPassword = getCurrentPassword();
            if (oldPassword !== currentPassword) { alert('❌ पुराना पासवर्ड गलत है!'); return; }
            if (newPassword.length < 4) { alert('❌ नया पासवर्ड कम से कम 4 अक्षर का होना चाहिए!'); return; }
            if (newPassword !== confirmPassword) { alert('❌ नया पासवर्ड और कन्फर्म पासवर्ड एक जैसे नहीं हैं!'); return; }
            setNewPassword(newPassword);
            alert('✅ पासवर्ड सफलतापूर्वक बदल दिया गया!');
            document.getElementById('changePasswordModal').classList.remove('active');
            document.getElementById('oldPasswordInput').value = '';
            document.getElementById('newPasswordInput').value = '';
            document.getElementById('confirmNewPasswordInput').value = '';
        }

        function openPasswordModal() { document.getElementById('deletePasswordInput').value = ''; document.getElementById('passwordModal').classList.add('active'); }
        function openChangePasswordModal() { document.getElementById('oldPasswordInput').value = ''; document.getElementById('newPasswordInput').value = ''; document.getElementById('confirmNewPasswordInput').value = ''; document.getElementById('changePasswordModal').classList.add('active'); }

        function verifyAndDelete() {
            const enteredPassword = document.getElementById('deletePasswordInput').value;
            const currentPassword = getCurrentPassword();
            if (enteredPassword === currentPassword) {
                document.getElementById('passwordModal').classList.remove('active');
                if (confirm('⚠️ क्या आप वाकई सभी चंदा और खर्च का डेटा हटाना चाहते हैं? यह क्रिया वापस नहीं ली जा सकती!')) deleteAllData();
            } else { alert('❌ गलत पासवर्ड! डेटा डिलीट नहीं किया जा सका।'); }
        }

        function escapeHtml(str) { if(!str) return ''; return str.replace(/[&<>]/g, function(m){ if(m==='&') return '&amp;'; if(m==='<') return '&lt;'; if(m==='>') return '&gt;'; return m; }); }

        function addDonation(name, village, amount, date) {
            if (!name || amount <= 0 || !date) return false;
            donations.push({ id: Date.now() + Math.random(), name: name.trim(), village: village.trim(), amount: parseFloat(amount), date: date });
            persist(); recalcTotals(); refreshListModals(); showToast('✅ नया चंदा जुड़ गया!'); return true;
        }
        function addExpense(name, amount, date) {
            if (!name || amount <= 0 || !date) return false;
            expenses.push({ id: Date.now() + Math.random(), name: name.trim(), amount: parseFloat(amount), date: date });
            persist(); recalcTotals(); refreshListModals(); showToast('✅ नया खर्च जुड़ गया!'); return true;
        }

        function backupData() {
            const data = { donations, expenses, backupDate: new Date().toISOString() };
            const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
            const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = `gram_backup_${new Date().toISOString().slice(0,19)}.json`; a.click(); URL.revokeObjectURL(blob);
            showToast('📁 बैकअप सेव हो गया!');
        }

        function exportDonationCSV() {
            if(donations.length === 0) { alert('कोई चंदा डेटा नहीं है'); return; }
            const headers = ['क्र.सं.', 'देनदार का नाम', 'गाँव', 'राशि (₹)', 'तारीख'];
            const rows = donations.map((d, idx) => [idx+1, d.name, d.village||'', d.amount, d.date]);
            const csvContent = [headers, ...rows].map(row => row.map(cell => `"${cell}"`).join(',')).join('\n');
            const blob = new Blob(["\uFEFF" + csvContent], { type: 'text/csv;charset=utf-8;' });
            const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = `chanda_data_${new Date().toISOString().slice(0,19)}.csv`; a.click(); URL.revokeObjectURL(blob);
            showToast('📄 चंदा CSV डाउनलोड हो रहा है');
        }

        function exportExpenseCSV() {
            if(expenses.length === 0) { alert('कोई खर्च डेटा नहीं है'); return; }
            const headers = ['क्र.सं.', 'खर्च का नाम', 'राशि (₹)', 'तारीख'];
            const rows = expenses.map((e, idx) => [idx+1, e.name, e.amount, e.date]);
            const csvContent = [headers, ...rows].map(row => row.map(cell => `"${cell}"`).join(',')).join('\n');
            const blob = new Blob(["\uFEFF" + csvContent], { type: 'text/csv;charset=utf-8;' });
            const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = `kharch_data_${new Date().toISOString().slice(0,19)}.csv`; a.click(); URL.revokeObjectURL(blob);
            showToast('📄 खर्च CSV डाउनलोड हो रहा है');
        }

        function exportExcel() {
            const donationSheetData = donations.map((d, idx) => ({ 'क्र.सं.': idx + 1, 'देनदार का नाम': d.name, 'गाँव': d.village||'', 'राशि (₹)': d.amount, 'तारीख': d.date }));
            const expenseSheetData = expenses.map((e, idx) => ({ 'क्र.सं.': idx + 1, 'खर्च का नाम': e.name, 'राशि (₹)': e.amount, 'तारीख': e.date }));
            const summaryData = [{ 'विवरण': 'कुल चंदा', 'राशि (₹)': totalDonation }, { 'विवरण': 'कुल खर्च', 'राशि (₹)': totalExpense }, { 'विवरण': 'शेष राशि', 'राशि (₹)': totalDonation - totalExpense }];
            const wb = XLSX.utils.book_new();
            const donationWs = XLSX.utils.json_to_sheet(donationSheetData); donationWs['!cols'] = [{wch:8}, {wch:25}, {wch:20}, {wch:12}, {wch:12}];
            XLSX.utils.book_append_sheet(wb, donationWs, 'चंदा');
            const expenseWs = XLSX.utils.json_to_sheet(expenseSheetData); expenseWs['!cols'] = [{wch:8}, {wch:25}, {wch:12}, {wch:12}];
            XLSX.utils.book_append_sheet(wb, expenseWs, 'खर्च');
            const summaryWs = XLSX.utils.json_to_sheet(summaryData); XLSX.utils.book_append_sheet(wb, summaryWs, 'सारांश');
            XLSX.writeFile(wb, `gram_samiti_${new Date().toISOString().slice(0,19)}.xlsx`);
            showToast('📊 Excel फाइल डाउनलोड हो रही है');
        }

        function printReport() {
            const win = window.open('', '_blank');
            win.document.write(`<!DOCTYPE html><html><head><title>ग्राम समिति रिपोर्ट - खेल सिंह</title><meta charset="UTF-8"><style>
                @page { size: A4; margin: 1.8cm; @top-left { content: "खेल सिंह"; font-size: 11pt; font-weight: bold; } @top-right { content: "0000000000"; font-size: 11pt; font-weight: bold; } @bottom-left { content: "ग्राम समिति रजिस्टर"; font-size: 9pt; } @bottom-right { content: "पृष्ठ " counter(page); font-size: 9pt; } }
                body { font-family: 'Inter', sans-serif; } .header { text-align: center; margin-bottom: 25px; border-bottom: 2px solid #1b5e4d; } h2 { text-align: center; color: #1b5e4d; background: #eef2f5; padding: 8px; } table { width: 100%; border-collapse: collapse; } th, td { border: 1px solid #aaa; padding: 8px; text-align: center; } th { background: #e9ecef; } .summary-box { margin-top: 30px; padding: 15px; border: 1px solid #1b5e4d; text-align: center; }
            </style></head><body>
            <div class="header"><h1>📋 ग्राम धनपुरी समिति रजिस्टर</h1><p>ग्राम धनपुरी - खेल सिंह (अध्यक्ष) | मोबाइल: 9343931468</p></div>
            <h2>💰 चंदा विवरण</h2><table><thead><tr><th>क्र.सं.</th><th>देनदार का नाम</th><th>गाँव</th><th>राशि (₹)</th><th>तारीख</th></tr></thead><tbody>${donations.map((d, idx) => `<tr><td>${idx+1}</td><td>${escapeHtml(d.name)}</td><td>${escapeHtml(d.village||'-')}</td><td>₹${d.amount.toFixed(2)}</td><td>${d.date}</td></tr>`).join('') || '<tr><td colspan="5">कोई डेटा नहीं</td></tr>'}</tbody></table>
            <h2>💸 खर्च विवरण</h2><table><thead><tr><th>क्र.सं.</th><th>खर्च का नाम</th><th>राशि (₹)</th><th>तारीख</th></tr></thead><tbody>${expenses.map((e, idx) => `<tr><td>${idx+1}</td><td>${escapeHtml(e.name)}</td><td>₹${e.amount.toFixed(2)}</td><td>${e.date}</td></tr>`).join('') || '<tr><td colspan="4">कोई डेटा नहीं</td></tr>'}</tbody></table>
            <div class="summary-box"><p><strong>📊 कुल चंदा:</strong> ₹${totalDonation.toFixed(2)} &nbsp;| <strong>📉 कुल खर्च:</strong> ₹${totalExpense.toFixed(2)} &nbsp;| <strong>⚖️ शेष राशि:</strong> ₹${(totalDonation - totalExpense).toFixed(2)}</p></div>
            <div class="footer-note"><p>रिपोर्ट जनरेट: ${new Date().toLocaleString('hi-IN')}</p><p>खेल सिंह (अध्यक्ष) | हस्ताक्षर: ___________</p></div>
            </body></html>`);
            win.document.close(); win.focus(); win.print();
        }

        const donationModal = document.getElementById('donationModal');
        const expenseModal = document.getElementById('expenseModal');
        const donationListModal = document.getElementById('donationListModal');
        const expenseListModal = document.getElementById('expenseListModal');
        const editDonationModal = document.getElementById('editDonationModal');
        const editExpenseModal = document.getElementById('editExpenseModal');
        const passwordModal = document.getElementById('passwordModal');
        const changePasswordModal = document.getElementById('changePasswordModal');
        const todayStr = new Date().toISOString().split('T')[0];

        function closeModals() {
            donationModal.classList.remove('active'); expenseModal.classList.remove('active');
            donationListModal.classList.remove('active'); expenseListModal.classList.remove('active');
            editDonationModal.classList.remove('active'); editExpenseModal.classList.remove('active');
            passwordModal.classList.remove('active'); changePasswordModal.classList.remove('active');
        }

        document.getElementById('addDonationBtn').onclick = () => {
            document.getElementById('modalDonationName').value = '';
            document.getElementById('modalDonationVillage').value = '';
            document.getElementById('modalDonationAmount').value = '';
            document.getElementById('modalDonationDate').value = todayStr;
            donationModal.classList.add('active');
        };
        document.getElementById('addExpenseBtn').onclick = () => {
            document.getElementById('modalExpenseName').value = '';
            document.getElementById('modalExpenseAmount').value = '';
            document.getElementById('modalExpenseDate').value = todayStr;
            expenseModal.classList.add('active');
        };
        document.getElementById('viewDonationBtn').onclick = () => { renderDonationList(''); document.getElementById('donationSearchInput').value = ''; donationListModal.classList.add('active'); };
        document.getElementById('viewExpenseBtn').onclick = () => { renderExpenseList(''); document.getElementById('expenseSearchInput').value = ''; expenseListModal.classList.add('active'); };
        document.getElementById('deleteAllDataBtn').onclick = openPasswordModal;
        document.getElementById('changePasswordBtn').onclick = openChangePasswordModal;
        document.getElementById('navChangePassword').onclick = () => { closeSidebar(); openChangePasswordModal(); };
        document.getElementById('navDeleteAll').onclick = () => { closeSidebar(); openPasswordModal(); };

        const closeBtns = ['closeDonationModal', 'closeExpenseModal', 'closeDonationListModal', 'closeExpenseListModal', 'closeEditDonationModal', 'closeEditExpenseModal', 'closePasswordModal', 'closeChangePasswordModal', 'closeDonationListBtn', 'closeExpenseListBtn', 'cancelDeleteBtn', 'cancelPasswordBtn'];
        closeBtns.forEach(id => { const el = document.getElementById(id); if(el) el.onclick = closeModals; });
        document.getElementById('cancelEditDonationBtn').onclick = () => editDonationModal.classList.remove('active');
        document.getElementById('cancelEditExpenseBtn').onclick = () => editExpenseModal.classList.remove('active');
        document.getElementById('confirmDeleteBtn').onclick = verifyAndDelete;
        document.getElementById('savePasswordBtn').onclick = changePassword;
        window.onclick = e => { if(e.target.classList.contains('modal')) closeModals(); };

        document.getElementById('saveDonationModalBtn').onclick = () => {
            const name = document.getElementById('modalDonationName').value.trim();
            const village = document.getElementById('modalDonationVillage').value.trim();
            const amount = parseFloat(document.getElementById('modalDonationAmount').value);
            const date = document.getElementById('modalDonationDate').value;
            if(addDonation(name, village, amount, date)) donationModal.classList.remove('active');
            else alert('कृपया नाम, सही राशि और तारीख भरें');
        };
        document.getElementById('saveExpenseModalBtn').onclick = () => {
            const name = document.getElementById('modalExpenseName').value.trim();
            const amount = parseFloat(document.getElementById('modalExpenseAmount').value);
            const date = document.getElementById('modalExpenseDate').value;
            if(addExpense(name, amount, date)) expenseModal.classList.remove('active');
            else alert('कृपया खर्च का नाम, सही राशि और तारीख भरें');
        };
        document.getElementById('saveEditDonationBtn').onclick = saveEditDonation;
        document.getElementById('saveEditExpenseBtn').onclick = saveEditExpense;

        document.getElementById('donationSearchInput')?.addEventListener('input', (e) => renderDonationList(e.target.value));
        document.getElementById('expenseSearchInput')?.addEventListener('input', (e) => renderExpenseList(e.target.value));

        document.getElementById('backupBtn').onclick = backupData;
        document.getElementById('exportDonationCSVBtn').onclick = exportDonationCSV;
        document.getElementById('exportExpenseCSVBtn').onclick = exportExpenseCSV;
        document.getElementById('exportExcelBtn').onclick = exportExcel;
        document.getElementById('printReportBtn').onclick = printReport;
        document.getElementById('restoreFileInput').onchange = e => { if(e.target.files.length) mergeRestoreData(e.target.files[0]); e.target.value = ''; };
        document.querySelector('label[for="restoreFileInput"]').onclick = () => document.getElementById('restoreFileInput').click();

        const menuToggle = document.getElementById('menuToggle');
        const sidebar = document.getElementById('sidebar');
        const overlay = document.getElementById('sidebarOverlay');
        function closeSidebar() { sidebar.classList.remove('open'); overlay.classList.remove('active'); }
        function openSidebar() { sidebar.classList.add('open'); overlay.classList.add('active'); }
        menuToggle.onclick = () => { if(sidebar.classList.contains('open')) closeSidebar(); else openSidebar(); };
        overlay.onclick = closeSidebar;
        document.getElementById('navBackupRestore')?.addEventListener('click', () => { closeSidebar(); document.getElementById('backupCard')?.scrollIntoView({ behavior: 'smooth' }); });
        document.getElementById('navExportImport')?.addEventListener('click', () => { closeSidebar(); document.getElementById('backupCard')?.scrollIntoView({ behavior: 'smooth' }); });
        document.getElementById('navPrintReport')?.addEventListener('click', () => { closeSidebar(); printReport(); });

        loadData();
    </script>
</body>
</html>
