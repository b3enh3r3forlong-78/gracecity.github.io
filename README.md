<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Church Service Reports</title>

<style>
:root{
    --primary:#2563eb;
    --success:#10b981;
    --warning:#f59e0b;
    --danger:#dc2626;
    --bg:#f8fafc;
    --card:#ffffff;
    --border:#e2e8f0;
}
* { box-sizing:border-box; }
body{
    margin:0;
    font-family:'Segoe UI',Tahoma,Geneva,Verdana,sans-serif;
    background:linear-gradient(135deg, var(--bg) 0%, #e2e8f0 100%);
    min-height:100vh;
}
.wrapper{
    max-width:1200px;
    margin:auto;
    padding:20px;
}
header{
    background:linear-gradient(135deg, var(--primary), #3b82f6);
    color:white;
    padding:30px;
    border-radius:20px;
    text-align:center;
    box-shadow:0 10px 30px rgba(37,99,235,.3);
    margin-bottom:30px;
}
.main{
    display:grid;
    grid-template-columns:380px 1fr;
    gap:25px;
}
.card{
    background:var(--card);
    padding:25px;
    border-radius:16px;
    box-shadow:0 4px 20px rgba(0,0,0,.08);
    border:1px solid var(--border);
}
h2{
    margin:0 0 20px 0;
    color:#1e293b;
    font-size:1.4em;
    display:flex;
    align-items:center;
    gap:10px;
}
h2 svg{ width:24px; height:24px; }
label{
    font-weight:600;
    margin:15px 0 5px 0;
    display:block;
    color:#475569;
    font-size:.95em;
}
input, select{
    width:100%;
    padding:12px 16px;
    border-radius:10px;
    border:2px solid var(--border);
    font-size:16px;
    transition:all .2s;
    background:#f8fafc;
}
input:focus, select:focus{
    outline:none;
    border-color:var(--primary);
    box-shadow:0 0 0 3px rgba(37,99,235,.1);
    background:white;
}
button{
    width:100%;
    padding:14px;
    margin-top:20px;
    background:linear-gradient(135deg, var(--primary), #3b82f6);
    color:white;
    border:none;
    border-radius:10px;
    cursor:pointer;
    font-size:16px;
    font-weight:600;
    transition:all .2s;
}
button:hover{ transform:translateY(-1px); box-shadow:0 8px 25px rgba(37,99,235,.3); }
button.small{
    width:auto;
    padding:8px 16px;
    margin:10px 0 0 0;
    font-size:14px;
}
.danger{ background:linear-gradient(135deg, var(--danger), #ef4444); }
.success{ background:linear-gradient(135deg, var(--success), #059669); }
.totals{
    background:linear-gradient(135deg, #eff6ff, #dbeafe);
    padding:20px;
    border-radius:12px;
    margin:20px 0;
    text-align:center;
    font-weight:600;
    border:2px solid rgba(37,99,235,.2);
}
.totals span{ 
    background:linear-gradient(135deg, var(--primary), #3b82f6);
    color:white;
    padding:8px 16px;
    border-radius:25px;
    font-size:1.3em;
    font-weight:700;
}
.offerings-section{
    background:linear-gradient(135deg, #fef3c7, #fde68a);
    border:2px solid rgba(245,158,11,.3);
    border-radius:12px;
    padding:20px;
    margin:20px 0;
}
.offering-tab{
    flex:1;
    padding:12px;
    background:#fef3c7;
    border:none;
    cursor:pointer;
    font-weight:600;
    transition:all .2s;
    border-radius:8px 8px 0 0;
    margin-bottom:5px;
}
.offering-tab.active{
    background:linear-gradient(135deg, var(--warning), #fbbf24);
    color:white;
}
.offering-panel{
    display:none;
    padding:15px;
    background:#fff;
    border-radius:0 0 12px 12px;
    border:2px solid rgba(245,158,11,.2);
    border-top:none;
}
.offering-panel.active{
    display:block;
}
.offering-list{
    max-height:150px;
    overflow-y:auto;
    margin:10px 0;
    background:#f8fafc;
    border-radius:8px;
    padding:10px;
}
.offering-item{
    background:white;
    padding:12px;
    border-radius:8px;
    margin:8px 0;
    display:flex;
    justify-content:space-between;
    align-items:center;
    border-left:4px solid var(--warning);
    box-shadow:0 2px 4px rgba(0,0,0,0.1);
}
.offering-amount{
    font-weight:700;
    color:var(--warning);
    font-size:1.1em;
}
.year-tabs{
    display:flex;
    flex-wrap:wrap;
    gap:10px;
    margin-bottom:20px;
}
.year-tab{
    padding:12px 20px;
    border-radius:12px;
    border:2px solid var(--border);
    background:#f8fafc;
    cursor:pointer;
    font-weight:600;
    font-size:15px;
    transition:all .2s;
}
.year-tab.active,
.year-tab:hover{
    background:linear-gradient(135deg, var(--primary), #3b82f6);
    color:white;
    border-color:var(--primary);
    transform:translateY(-2px);
}
.year-stats{
    background:linear-gradient(135deg, #f0fdf4, #dcfce7);
    padding:25px;
    border-radius:16px;
    margin-bottom:25px;
    text-align:center;
    border:2px solid rgba(16,185,129,.3);
}
.year-table{
    width:100%;
    border-collapse:separate;
    border-spacing:0 8px;
    margin-top:10px;
}
.year-table th{
    background:linear-gradient(135deg, var(--primary), #3b82f6);
    color:white;
    padding:16px 12px;
    text-align:left;
    border-radius:12px 12px 0 0;
    font-weight:600;
}
.year-table td{
    padding:16px 12px;
    background:#f8fafc;
    border-radius:12px;
}
.avg-tr td{
    background:linear-gradient(135deg, var(--warning), #fbbf24) !important;
    color:#92400e;
    font-weight:700;
}
@media(max-width:900px){
    .main{ grid-template-columns:1fr; gap:20px; }
    .year-tabs{ justify-content:center; }
}
.loading{ text-align:center; color:#64748b; font-style:italic; padding:40px; }
</style>
</head>

<body>
<div class="wrapper">
<header>
<h1>🏛 GRACE CITY PRAMPRAM</h1>
<p><strong>Complete Attendance Tracking</strong> • Yearly Analytics • Smart Insights</p>
<p><b>WE GIVE YOUR LIFE A MEANING</b></p>
</header>

<div class="main">
<!-- ENTRY FORM -->
<div class="card">
<h2>📝 New Service</h2>
<form id="serviceForm">
<label>Date</label>
<input type="date" id="date" required>

<label>Service Type</label>
<input type="text" id="title" placeholder="e.g., Sunday Service, Joint Service" required>

<label>Male</label>
<input type="number" id="male" min="0" value="0">

<label>Female</label>
<input type="number" id="female" min="0" value="0">

<label>Children</label>
<input type="number" id="children" min="0" value="0">

<label>First Timers</label>
<input type="number" id="firstTimers" min="0" value="0">

<!-- OFFERINGS - SIMPLIFIED & FIXED -->
<div class="offerings-section">
    <h3 style="margin:0 0 15px 0; color:var(--warning);">💰 Offerings</h3>
    
    <div style="display:flex; gap:10px; margin-bottom:15px;">
        <button type="button" class="offering-tab active" id="offeringTab">Offerings</button>
        <button type="button" class="offering-tab" id="rhapsodyTab">Rhapsody</button>
    </div>
    
    <div id="offeringPanel" class="offering-panel active">
        <label>Amount (₵)</label>
        <input type="number" id="offeringAmount" min="0" step="0.5" placeholder="0.00">
        <label>Notes</label>
        <input type="text" id="offeringNotes" placeholder="e.g., Sunday offering">
        <button type="button" class="small success" id="addOffering">➕ Add Offering</button>
    </div>
    
    <div id="rhapsodyPanel" class="offering-panel">
        <label>Amount (₵)</label>
        <input type="number" id="rhapsodyAmount" min="0" step="0.5" placeholder="0.00">
        <label>Notes</label>
        <input type="text" id="rhapsodyNotes" placeholder="e.g., Monthly rhapsody">
        <button type="button" class="small success" id="addRhapsody">➕ Add Rhapsody</button>
    </div>
    
    <div id="offeringsList" class="offering-list">
        <div style="color:#64748b;text-align:center;padding:20px;">No offerings added</div>
    </div>
    <div id="offeringsTotal" class="totals" style="display:none;">
        Total: <span id="totalAmount">0</span> ₵
    </div>
</div>

<div class="totals" id="attendanceTotal" style="display:none;">
    Total Attendance: <span id="totalAtt">0</span>
</div>

<button type="submit">💾 Save Service Report</button>
</form>
</div>

<!-- ANALYTICS -->
<div class="card">
<h2>📊 Analytics Dashboard</h2>
<div class="year-tabs" id="yearTabs"></div>
<div id="analyticsContent" class="loading">Loading reports...</div>
<button class="success" id="exportData">📤 Export CSV</button>
<button class="danger" id="clearData" style="margin-top:10px;">🗑️ Clear All</button>
</div>
</div>
</div>

<script>
// GLOBAL STATE
const STORAGE_KEY = "churchReportsV2";
let offerings = [];

// DATA FUNCTIONS
function getReports() {
    try {
        return JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
    } catch {
        return [];
    }
}

function saveReports(data) {
    try {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
        return true;
    } catch {
        alert("Storage error!");
        return false;
    }
}

// ATTENDANCE CALCULATION
function updateAttendance() {
    const male = parseFloat(document.getElementById('male').value) || 0;
    const female = parseFloat(document.getElementById('female').value) || 0;
    const children = parseFloat(document.getElementById('children').value) || 0;
    const total = male + female + children;
    
    document.getElementById('totalAtt').textContent = total.toLocaleString();
    document.getElementById('attendanceTotal').style.display = total > 0 ? 'block' : 'none';
}

// OFFERINGS FUNCTIONS - COMPLETELY REWRITTEN
function switchOfferingTab(activeTab, inactiveTab, activePanel, inactivePanel) {
    document.getElementById(activeTab).classList.add('active');
    document.getElementById(inactiveTab).classList.remove('active');
    document.getElementById(activePanel).classList.add('active');
    document.getElementById(inactivePanel).classList.remove('active');
}

function addOfferingItem(type) {
    const amountId = type === 'offerings' ? 'offeringAmount' : 'rhapsodyAmount';
    const notesId = type === 'offerings' ? 'offeringNotes' : 'rhapsodyNotes';
    
    const amount = parseFloat(document.getElementById(amountId).value) || 0;
    const notes = document.getElementById(notesId).value.trim();
    
    if (amount <= 0) {
        alert('Please enter amount greater than 0');
        return;
    }
    
    offerings.push({ type: type.charAt(0).toUpperCase() + type.slice(1), amount, notes });
    updateOfferingsDisplay();
    
    // Clear inputs
    document.getElementById(amountId).value = '';
    document.getElementById(notesId).value = '';
}

function updateOfferingsDisplay() {
    const list = document.getElementById('offeringsList');
    const totalEl = document.getElementById('totalAmount');
    const totalContainer = document.getElementById('offeringsTotal');
    
    if (offerings.length === 0) {
        list.innerHTML = '<div style="color:#64748b;text-align:center;padding:20px;">No offerings added</div>';
        totalContainer.style.display = 'none';
        return;
    }
    
    list.innerHTML = offerings.map((item, index) => `
        <div class="offering-item">
            <div>
                <div>${item.type}: <span class="offering-amount">₵${item.amount.toLocaleString()}</span></div>
                ${item.notes ? `<small>${item.notes}</small>` : ''}
            </div>
            <button type="button" class="small danger" onclick="removeOffering(${index})">❌</button>
        </div>
    `).join('');
    
    const total = offerings.reduce((sum, item) => sum + item.amount, 0);
    totalEl.textContent = total.toLocaleString();
    totalContainer.style.display = 'block';
}

function removeOffering(index) {
    offerings.splice(index, 1);
    updateOfferingsDisplay();
}

// YEAR ANALYTICS
function loadYears() {
    const reports = getReports();
    const years = [...new Set(reports.map(r => r.year))].sort((a, b) => b - a);
    const tabsContainer = document.getElementById('yearTabs');
    
    tabsContainer.innerHTML = '';
    
    if (years.length === 0) {
        tabsContainer.innerHTML = '<div style="width:100%;text-align:center;color:#64748b;padding:20px;">No reports yet</div>';
        document.getElementById('analyticsContent').innerHTML = '<div class="loading">Add your first service!</div>';
        return;
    }
    
    years.forEach(year => {
        const tab = document.createElement('div');
        tab.className = 'year-tab';
        tab.textContent = `${year} (${reports.filter(r => r.year === year).length})`;
        tab.onclick = () => showYearData(year);
        tabsContainer.appendChild(tab);
    });
    
    // Show first year
    if (years.length > 0) showYearData(years[0]);
}

function showYearData(year) {
    // Update active tab
    document.querySelectorAll('.year-tab').forEach(tab => tab.classList.remove('active'));
    event.target.classList.add('active');
    
    const reports = getReports().filter(r => r.year === year)
        .sort((a, b) => new Date(b.date) - new Date(a.date));
    
    const content = document.getElementById('analyticsContent');
    
    if (reports.length === 0) {
        content.innerHTML = `<p style="color:#64748b;text-align:center;padding:40px;">No services in ${year}</p>`;
        return;
    }
    
    // Calculate stats
    const totalServices = reports.length;
    const totalAttendance = reports.reduce((sum, r) => sum + r.totalAttendance, 0);
    const avgAttendance = Math.round(totalAttendance / totalServices);
    const totalOfferings = reports.reduce((sum, r) => sum + (r.offeringsTotal || 0), 0);
    
    let html = `
        <div class="year-stats">
            <h3>${year} Report</h3>
            <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:15px;">
                <div><strong>${totalServices}</strong> Services</div>
                <div><strong>${totalAttendance.toLocaleString()}</strong> Attendance</div>
                <div><strong>${avgAttendance}</strong> Average</div>
                <div><strong>₵${totalOfferings.toLocaleString()}</strong> Offerings</div>
            </div>
        </div>
        <table class="year-table">
            <thead><tr>
                <th>Date</th><th>Service</th><th>Male</th><th>Female</th>
                <th>Children</th><th>First Timers</th><th>Offerings</th><th>Total</th>
            </tr></thead>
            <tbody>
    `;
    
    reports.forEach(r => {
        const offeringsText = r.offeringsTotal ? `₵${r.offeringsTotal.toLocaleString()}` : '-';
        html += `
            <tr>
                <td>${new Date(r.date).toLocaleDateString('en-GH')}</td>
                <td>${r.title}</td>
                <td>${r.male}</td>
                <td>${r.female}</td>
                <td>${r.children}</td>
                <td style="color:var(--success);">${r.firstTimers}</td>
                <td style="color:var(--warning);font-weight:700;">${offeringsText}</td>
                <td style="font-weight:700;">${r.totalAttendance}</td>
            </tr>`;
    });
    
    html += `
            </tbody><tfoot><tr class="avg-tr">
                <td colspan="2"><strong>TOTALS</strong></td>
                <td><strong>${reports.reduce((s,r)=>s+r.male,0)}</strong></td>
                <td><strong>${reports.reduce((s,r)=>s+r.female,0)}</strong></td>
                <td><strong>${reports.reduce((s,r)=>s+r.children,0)}</strong></td>
                <td><strong>${reports.reduce((s,r)=>s+r.firstTimers,0)}</strong></td>
                <td><strong>₵${totalOfferings.toLocaleString()}</strong></td>
                <td><strong>${totalAttendance.toLocaleString()}</strong></td>
            </tr></tfoot></table>`;
    
    content.innerHTML = html;
}

// EVENT LISTENERS - ALL PROPERLY BOUND
document.addEventListener('DOMContentLoaded', function() {
    // Form inputs
    ['male','female','children','firstTimers'].forEach(id => {
        document.getElementById(id).addEventListener('input', updateAttendance);
    });
    
    // Offering tabs
    document.getElementById('offeringTab').onclick = () => 
        switchOfferingTab('offeringTab', 'rhapsodyTab', 'offeringPanel', 'rhapsodyPanel');
    document.getElementById('rhapsodyTab').onclick = () => 
        switchOfferingTab('rhapsodyTab', 'offeringTab', 'rhapsodyPanel', 'offeringPanel');
    
    // Add offerings
    document.getElementById('addOffering').onclick = () => addOfferingItem('offerings');
    document.getElementById('addRhapsody').onclick = () => addOfferingItem('rhapsody');
    
    // Save form
    document.getElementById('serviceForm').onsubmit = function(e) {
        e.preventDefault();
        
        const formData = {
            id: Date.now(),
            date: document.getElementById('date').value,
            title: document.getElementById('title').value.trim(),
            male: parseFloat(document.getElementById('male').value) || 0,
            female: parseFloat(document.getElementById('female').value) || 0,
            children: parseFloat(document.getElementById('children').value) || 0,
            firstTimers: parseFloat(document.getElementById('firstTimers').value) || 0,
            offerings: [...offerings],
            offeringsTotal: offerings.reduce((sum, o) => sum + o.amount, 0),
            year: new Date(document.getElementById('date').value).getFullYear(),
            totalAttendance: 0
        };
        
        formData.totalAttendance = formData.male + formData.female + formData.children;
        
        const reports = getReports();
        reports.unshift(formData);
        
        if (saveReports(reports)) {
            alert(`✅ "${formData.title}" saved!`);
            document.getElementById('serviceForm').reset();
            document.getElementById('date').valueAsDate = new Date();
            offerings = [];
            updateOfferingsDisplay();
            updateAttendance();
            loadYears();
        }
    };
    
    // Export & Clear
    document.getElementById('exportData').onclick = function() {
        const reports = getReports();
        if (!reports.length) return alert('No data');
        
        const csv = ['Date,Service,Male,Female,Children,FirstTimers,Offerings,Total', 
            ...reports.map(r => `"${r.date}","${r.title}","${r.male}","${r.female}","${r.children}","${r.firstTimers}","${r.offeringsTotal||0}","${r.totalAttendance}"`)].join('\n');
        const blob = new Blob([csv], {type: 'text/csv'});
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = `Church_${new Date().getFullYear()}.csv`;
        a.click();
    };
    
    document.getElementById('clearData').onclick = function() {
        if (confirm('Delete ALL data?')) {
            localStorage.removeItem(STORAGE_KEY);
            offerings = [];
            loadYears();
            alert('Data cleared');
        }
    };
    
    // Initialize
    document.getElementById('date').valueAsDate = new Date();
    loadYears();
});
</script>

<footer style="text-align:center; padding:20px; color:#64748b; font-size:14px;">
    <p>© 2026 Grace City Prampram. All Rights Reserved.</p>
</footer>
</body>
</html>
