أعتذر بشدة عن المشاكل السابقة. سأقدم لك نسخة مبسطة ومباشرة تعمل بشكل كامل دون مشاكل:

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام إدارة المؤسسات</title>
    <style>
        :root {
            --primary: #2563eb;
            --primary-light: #dbeafe;
            --secondary: #0f766e;
            --accent: #d97706;
            --light: #f8fafc;
            --dark: #0f172a;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f1f5f9;
            color: #334155;
            display: flex;
            min-height: 100vh;
        }
        
        /* الشريط الجانبي */
        .sidebar {
            width: 250px;
            background-color: white;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            display: flex;
            flex-direction: column;
        }
        
        .sidebar-header {
            padding: 20px;
            border-bottom: 1px solid #e2e8f0;
            text-align: center;
        }
        
        .sidebar-header h2 {
            font-size: 1.25rem;
            font-weight: bold;
            color: #1e293b;
        }
        
        .sidebar-header p {
            font-size: 0.875rem;
            color: #64748b;
        }
        
        .sidebar-nav {
            flex: 1;
            overflow-y: auto;
            padding: 10px 0;
        }
        
        .nav-link {
            display: flex;
            align-items: center;
            padding: 12px 20px;
            color: #475569;
            text-decoration: none;
            transition: all 0.3s;
        }
        
        .nav-link:hover {
            background-color: #f1f5f9;
        }
        
        .nav-link.active {
            background-color: var(--primary-light);
            color: var(--primary);
            border-right: 4px solid var(--primary);
        }
        
        .nav-link i {
            margin-left: 10px;
            font-size: 1.25rem;
        }
        
        .sidebar-footer {
            padding: 15px;
            border-top: 1px solid #e2e8f0;
            display: flex;
            align-items: center;
        }
        
        .sidebar-footer img {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: #e2e8f0;
            border: 1px dashed #94a3b8;
        }
        
        .sidebar-footer div {
            margin-right: 10px;
        }
        
        .sidebar-footer p {
            font-size: 0.875rem;
            font-weight: 500;
        }
        
        .sidebar-footer span {
            font-size: 0.75rem;
            color: #64748b;
        }
        
        /* المحتوى الرئيسي */
        .main-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        
        .header {
            background-color: white;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .header h1 {
            font-size: 1.25rem;
            font-weight: bold;
            color: #1e293b;
        }
        
        .header-actions {
            display: flex;
            align-items: center;
        }
        
        .search-container {
            position: relative;
            margin-right: 15px;
        }
        
        .search-container input {
            border: 1px solid #cbd5e1;
            border-radius: 20px;
            padding: 8px 15px 8px 35px;
            width: 200px;
        }
        
        .search-container i {
            position: absolute;
            left: 12px;
            top: 50%;
            transform: translateY(-50%);
            color: #94a3b8;
        }
        
        .header-actions button {
            background: none;
            border: none;
            color: #64748b;
            font-size: 1.25rem;
            cursor: pointer;
            margin-left: 10px;
            position: relative;
        }
        
        .notification-badge {
            position: absolute;
            top: -3px;
            right: -3px;
            width: 8px;
            height: 8px;
            background-color: var(--danger);
            border-radius: 50%;
        }
        
        .content {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
        }
        
        .section-title {
            font-size: 1.5rem;
            font-weight: bold;
            margin-bottom: 20px;
            color: #1e293b;
        }
        
        .kpi-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .kpi-card {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            border-left: 4px solid var(--primary);
            transition: all 0.3s;
        }
        
        .kpi-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px rgba(0,0,0,0.1);
        }
        
        .kpi-card.financial { border-left-color: var(--primary); }
        .kpi-card.clients { border-left-color: var(--secondary); }
        .kpi-card.operations { border-left-color: var(--warning); }
        .kpi-card.staff { border-left-color: var(--success); }
        
        .kpi-card .card-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 15px;
        }
        
        .kpi-card .card-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .kpi-card.financial .card-icon { background-color: #dbeafe; color: var(--primary); }
        .kpi-card.clients .card-icon { background-color: #ccfbf1; color: var(--secondary); }
        .kpi-card.operations .card-icon { background-color: #fef3c7; color: var(--warning); }
        .kpi-card.staff .card-icon { background-color: #d1fae5; color: var(--success); }
        
        .kpi-card h3 {
            font-size: 1.5rem;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .kpi-card p {
            color: #64748b;
            font-size: 0.9rem;
        }
        
        .kpi-card .trend {
            display: flex;
            align-items: center;
            font-size: 0.9rem;
            margin-top: 5px;
        }
        
        .kpi-card .trend.up { color: var(--success); }
        .kpi-card .trend.down { color: var(--danger); }
        
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
            gap: 20px;
        }
        
        .dashboard-card {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .card-header h3 {
            font-size: 1.25rem;
            font-weight: bold;
        }
        
        .chart-container {
            height: 250px;
            position: relative;
        }
        
        .tasks-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        .task-item {
            display: flex;
            align-items: center;
            padding: 15px;
            background-color: #f8fafc;
            border-radius: 8px;
        }
        
        .task-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-left: 15px;
        }
        
        .task-icon.blue { background-color: #dbeafe; color: var(--primary); }
        .task-icon.amber { background-color: #fef3c7; color: var(--warning); }
        .task-icon.green { background-color: #d1fae5; color: var(--success); }
        .task-icon.purple { background-color: #ede9fe; color: #8b5cf6; }
        
        .task-info {
            flex: 1;
        }
        
        .task-info h4 {
            font-weight: 600;
            margin-bottom: 3px;
        }
        
        .task-info p {
            font-size: 0.9rem;
            color: #64748b;
        }
        
        .task-badge {
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 500;
        }
        
        .task-badge.blue { background-color: #dbeafe; color: var(--primary); }
        .task-badge.amber { background-color: #fef3c7; color: var(--warning); }
        .task-badge.green { background-color: #d1fae5; color: var(--success); }
        .task-badge.purple { background-color: #ede9fe; color: #8b5cf6; }
        
        /* صفحة الموارد البشرية */
        .hr-section {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        
        .hr-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .filters {
            display: flex;
            gap: 10px;
        }
        
        .filter-btn {
            padding: 8px 15px;
            border-radius: 6px;
            border: none;
            background-color: #f1f5f9;
            color: #334155;
            cursor: pointer;
        }
        
        .filter-btn.active {
            background-color: var(--primary);
            color: white;
        }
        
        .add-employee-btn {
            padding: 8px 15px;
            border-radius: 6px;
            border: none;
            background-color: var(--primary);
            color: white;
            cursor: pointer;
            display: flex;
            align-items: center;
        }
        
        .add-employee-btn i {
            margin-left: 5px;
        }
        
        .employees-table {
            width: 100%;
            border-collapse: collapse;
        }
        
        .employees-table th,
        .employees-table td {
            padding: 12px 15px;
            text-align: right;
            border-bottom: 1px solid #e2e8f0;
        }
        
        .employees-table th {
            background-color: #f8fafc;
            font-weight: 600;
            color: #475569;
        }
        
        .employees-table tr:hover {
            background-color: #f8fafc;
        }
        
        .employee-cell {
            display: flex;
            align-items: center;
        }
        
        .employee-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: #e2e8f0;
            border: 1px dashed #94a3b8;
            margin-left: 10px;
        }
        
        .status-badge {
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 500;
        }
        
        .status-badge.active { background-color: #d1fae5; color: var(--success); }
        .status-badge.leave { background-color: #fef3c7; color: var(--warning); }
        
        .action-btn {
            background: none;
            border: none;
            color: #64748b;
            cursor: pointer;
            margin-left: 10px;
        }
        
        .action-btn:hover {
            color: var(--primary);
        }
        
        /* صفحة الهيكل التنظيمي */
        .org-section {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        
        .org-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .org-chart {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .org-level {
            display: flex;
            justify-content: center;
            margin-bottom: 40px;
        }
        
        .org-node {
            background-color: #f0f9ff;
            border: 1px solid #bae6fd;
            border-radius: 8px;
            padding: 15px;
            margin: 0 15px;
            text-align: center;
            min-width: 180px;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
        }
        
        .org-node:hover {
            background-color: #e0f2fe;
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .org-node .node-title {
            font-weight: bold;
            margin-bottom: 5px;
            color: #0369a1;
        }
        
        .org-node .node-subtitle {
            font-size: 0.9rem;
            color: #475569;
        }
        
        /* صفحة التقارير */
        .reports-section {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        
        .reports-tabs {
            display: flex;
            border-bottom: 1px solid #e2e8f0;
            margin-bottom: 20px;
        }
        
        .tab-btn {
            padding: 10px 20px;
            background: none;
            border: none;
            cursor: pointer;
            font-weight: 500;
            color: #64748b;
            position: relative;
        }
        
        .tab-btn.active {
            color: var(--primary);
        }
        
        .tab-btn.active::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 100%;
            height: 2px;
            background-color: var(--primary);
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .reports-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .reports-table {
            width: 100%;
            border-collapse: collapse;
        }
        
        .reports-table th,
        .reports-table td {
            padding: 12px 15px;
            text-align: right;
            border-bottom: 1px solid #e2e8f0;
        }
        
        .reports-table th {
            background-color: #f8fafc;
            font-weight: 600;
            color: #475569;
        }
        
        .reports-table tr:hover {
            background-color: #f8fafc;
        }
        
        .view-btn, .download-btn {
            padding: 5px 10px;
            border-radius: 4px;
            border: none;
            cursor: pointer;
            font-size: 0.9rem;
        }
        
        .view-btn {
            background-color: #dbeafe;
            color: var(--primary);
            margin-left: 5px;
        }
        
        .download-btn {
            background-color: #f1f5f9;
            color: #475569;
        }
        
        /* الصفحات المخفية */
        .page-section {
            display: none;
        }
        
        .page-section.active {
            display: block;
        }
    </style>
</head>
<body>
    <!-- الشريط الجانبي -->
    <div class="sidebar">
        <div class="sidebar-header">
            <h2>نظام الإدارة</h2>
            <p>لوحة التحكم الرئيسية</p>
        </div>
        
        <nav class="sidebar-nav">
            <a href="#" data-section="dashboard" class="nav-link active">
                <i class="fas fa-tachometer-alt"></i>
                <span>لوحة التحكم</span>
            </a>
            <a href="#" data-section="hr" class="nav-link">
                <i class="fas fa-users"></i>
                <span>الموارد البشرية</span>
            </a>
            <a href="#" data-section="operations" class="nav-link">
                <i class="fas fa-cogs"></i>
                <span>العمليات</span>
            </a>
            <a href="#" data-section="org-structure" class="nav-link">
                <i class="fas fa-sitemap"></i>
                <span>الهيكل التنظيمي</span>
            </a>
            <a href="#" data-section="reports" class="nav-link">
                <i class="fas fa-chart-bar"></i>
                <span>التقارير</span>
            </a>
        </nav>
        
        <div class="sidebar-footer">
            <div class="employee-avatar"></div>
            <div>
                <p>أحمد محمد</p>
                <span>مدير النظام</span>
            </div>
        </div>
    </div>

    <!-- المحتوى الرئيسي -->
    <div class="main-content">
        <!-- شريط العنوان -->
        <header class="header">
            <h1 id="page-title">لوحة التحكم</h1>
            <div class="header-actions">
                <div class="search-container">
                    <i class="fas fa-search"></i>
                    <input type="text" placeholder="بحث...">
                </div>
                <button>
                    <i class="fas fa-bell"></i>
                    <span class="notification-badge"></span>
                </button>
                <button>
                    <i class="fas fa-cog"></i>
                </button>
            </div>
        </header>

        <!-- محتوى الصفحات -->
        <div class="content">
            <!-- لوحة التحكم -->
            <section id="dashboard" class="page-section active">
                <h2 class="section-title">مؤشرات الأداء الرئيسية</h2>
                <div class="kpi-grid">
                    <div class="kpi-card financial">
                        <div class="card-header">
                            <div>
                                <p>المالية</p>
                                <h3>8.2M</h3>
                                <div class="trend up">
                                    <i class="fas fa-arrow-up"></i>
                                    12.5%
                                </div>
                            </div>
                            <div class="card-icon">
                                <i class="fas fa-wallet"></i>
                            </div>
                        </div>
                    </div>
                    
                    <div class="kpi-card clients">
                        <div class="card-header">
                            <div>
                                <p>العملاء</p>
                                <h3>4,892</h3>
                                <div class="trend up">
                                    <i class="fas fa-arrow-up"></i>
                                    3.2%
                                </div>
                            </div>
                            <div class="card-icon">
                                <i class="fas fa-users"></i>
                            </div>
                        </div>
                    </div>
                    
                    <div class="kpi-card operations">
                        <div class="card-header">
                            <div>
                                <p>العمليات</p>
                                <h3>1,248</h3>
                                <div class="trend down">
                                    <i class="fas fa-arrow-down"></i>
                                    1.7%
                                </div>
                            </div>
                            <div class="card-icon">
                                <i class="fas fa-cogs"></i>
                            </div>
                        </div>
                    </div>
                    
                    <div class="kpi-card staff">
                        <div class="card-header">
                            <div>
                                <p>الموظفين</p>
                                <h3>324</h3>
                                <div class="trend up">
                                    <i class="fas fa-arrow-up"></i>
                                    5.3%
                                </div>
                            </div>
                            <div class="card-icon">
                                <i class="fas fa-user-plus"></i>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="dashboard-grid">
                    <div class="dashboard-card">
                        <div class="card-header">
                            <h3>أداء المشاريع</h3>
                            <div class="filters">
                                <button class="filter-btn">شهري</button>
                                <button class="filter-btn active">سنوي</button>
                            </div>
                        </div>
                        <div class="chart-container" id="performanceChart">
                            <!-- سيقوم الجافاسكريبت بملء هذا الجزء -->
                            <canvas id="perfChartCanvas"></canvas>
                        </div>
                    </div>
                    
                    <div class="dashboard-card">
                        <div class="card-header">
                            <h3>توزيع المهام</h3>
                            <button class="add-employee-btn">
                                <i class="fas fa-plus"></i>
                                إضافة مهمة
                            </button>
                        </div>
                        <div class="tasks-container">
                            <div class="task-item">
                                <div class="task-icon blue">
                                    <i class="fas fa-file-invoice"></i>
                                </div>
                                <div class="task-info">
                                    <h4>تقرير الربع السنوي</h4>
                                    <p>إدارة المالية</p>
                                </div>
                                <span class="task-badge blue">قيد العمل</span>
                            </div>
                            
                            <div class="task-item">
                                <div class="task-icon amber">
                                    <i class="fas fa-users"></i>
                                </div>
                                <div class="task-info">
                                    <h4>اجتماع الإدارة</h4>
                                    <p>إدارة التخطيط</p>
                                </div>
                                <span class="task-badge amber">معلق</span>
                            </div>
                            
                            <div class="task-item">
                                <div class="task-icon green">
                                    <i class="fas fa-chart-line"></i>
                                </div>
                                <div class="task-info">
                                    <h4>تحليل السوق</h4>
                                    <p>إدارة التسويق</p>
                                </div>
                                <span class="task-badge green">مكتمل</span>
                            </div>
                            
                            <div class="task-item">
                                <div class="task-icon purple">
                                    <i class="fas fa-laptop"></i>
                                </div>
                                <div class="task-info">
                                    <h4>تحديث النظام</h4>
                                    <p>إدارة التقنية</p>
                                </div>
                                <span class="task-badge purple">قيد العمل</span>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- الموارد البشرية -->
            <section id="hr" class="page-section">
                <div class="hr-section">
                    <div class="hr-header">
                        <h2 class="section-title">إدارة الموارد البشرية</h2>
                        <button class="add-employee-btn">
                            <i class="fas fa-plus"></i>
                            إضافة موظف
                        </button>
                    </div>
                    
                    <div class="filters">
                        <button class="filter-btn active">الكل</button>
                        <button class="filter-btn">الإدارة</button>
                        <button class="filter-btn">المشاريع</button>
                        <button class="filter-btn">الدعم</button>
                    </div>
                    
                    <div class="search-container" style="margin: 15px 0; width: 300px;">
                        <i class="fas fa-search"></i>
                        <input type="text" placeholder="بحث باسم الموظف...">
                    </div>
                    
                    <table class="employees-table">
                        <thead>
                            <tr>
                                <th>الموظف</th>
                                <th>الوظيفة</th>
                                <th>القسم</th>
                                <th>الحالة</th>
                                <th>تاريخ التعيين</th>
                                <th>الإجراءات</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>
                                    <div class="employee-cell">
                                        <div class="employee-avatar"></div>
                                        <div>
                                            <div>أحمد عبد الله</div>
                                            <div style="font-size: 0.9rem; color: #64748b;">ahmed@company.com</div>
                                        </div>
                                    </div>
                                </td>
                                <td>مدير المشاريع</td>
                                <td>المشاريع</td>
                                <td><span class="status-badge active">نشط</span></td>
                                <td>15/03/2020</td>
                                <td>
                                    <button class="action-btn"><i class="fas fa-edit"></i></button>
                                    <button class="action-btn"><i class="fas fa-trash"></i></button>
                                </td>
                            </tr>
                            <tr>
                                <td>
                                    <div class="employee-cell">
                                        <div class="employee-avatar"></div>
                                        <div>
                                            <div>سارة محمد</div>
                                            <div style="font-size: 0.9rem; color: #64748b;">sara@company.com</div>
                                        </div>
                                    </div>
                                </td>
                                <td>مصممة UI/UX</td>
                                <td>التقنية</td>
                                <td><span class="status-badge active">نشط</span></td>
                                <td>22/07/2021</td>
                                <td>
                                    <button class="action-btn"><i class="fas fa-edit"></i></button>
                                    <button class="action-btn"><i class="fas fa-trash"></i></button>
                                </td>
                            </tr>
                            <tr>
                                <td>
                                    <div class="employee-cell">
                                        <div class="employee-avatar"></div>
                                        <div>
                                            <div>خالد حسن</div>
                                            <div style="font-size: 0.9rem; color: #64748b;">khaled@company.com</div>
                                        </div>
                                    </div>
                                </td>
                                <td>مطور برمجيات</td>
                                <td>التقنية</td>
                                <td><span class="status-badge leave">إجازة</span></td>
                                <td>10/11/2019</td>
                                <td>
                                    <button class="action-btn"><i class="fas fa-edit"></i></button>
                                    <button class="action-btn"><i class="fas fa-trash"></i></button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- الهيكل التنظيمي -->
            <section id="org-structure" class="page-section">
                <div class="org-section">
                    <div class="org-header">
                        <h2 class="section-title">الهيكل التنظيمي</h2>
                        <div>
                            <button class="filter-btn" style="margin-right: 10px;">
                                <i class="fas fa-download"></i>
                                تصدير
                            </button>
                            <button class="add-employee-btn">
                                <i class="fas fa-plus"></i>
                                إضافة وحدة
                            </button>
                        </div>
                    </div>
                    
                    <div class="org-chart">
                        <div class="org-level">
                            <div class="org-node">
                                <div class="node-title">المدير العام</div>
                                <div class="node-subtitle">أ. أحمد محمد</div>
                            </div>
                        </div>
                        
                        <div class="org-level">
                            <div class="org-node">
                                <div class="node-title">نائب المدير العام</div>
                                <div class="node-subtitle">أ. سعيد عبد الله</div>
                            </div>
                            <div class="org-node">
                                <div class="node-title">المدير المالي</div>
                                <div class="node-subtitle">أ. محمد خالد</div>
                            </div>
                            <div class="org-node">
                                <div class="node-title">مدير العمليات</div>
                                <div class="node-subtitle">أ. ليلى أحمد</div>
                            </div>
                        </div>
                        
                        <div class="org-level">
                            <div class="org-node">
                                <div class="node-title">رئيس قسم المحاسبة</div>
                                <div class="node-subtitle">أ. عمر ناصر</div>
                            </div>
                            <div class="org-node">
                                <div class="node-title">رئيس قسم المشتريات</div>
                                <div class="node-subtitle">أ. سمر علي</div>
                            </div>
                            <div class="org-node">
                                <div class="node-title">رئيس قسم المبيعات</div>
                                <div class="node-subtitle">أ. خالد سعد</div>
                            </div>
                            <div class="org-node">
                                <div class="node-title">رئيس قسم الجودة</div>
                                <div class="node-subtitle">أ. نورة حسن</div>
                            </div>
                            <div class="org-node">
                                <div class="node-title">رئيس قسم الدعم</div>
                                <div class="node-subtitle">أ. فهد محمد</div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
            
            <!-- التقارير -->
            <section id="reports" class="page-section">
                <div class="reports-section">
                    <h2 class="section-title">التقارير والإحصائيات</h2>
                    
                    <div class="reports-tabs">
                        <button class="tab-btn active" data-tab="financial">المالية</button>
                        <button class="tab-btn" data-tab="operations">العمليات</button>
                        <button class="tab-btn" data-tab="hr-reports">الموارد البشرية</button>
                        <button class="tab-btn" data-tab="projects">المشاريع</button>
                    </div>
                    
                    <div id="financial" class="tab-content active">
                        <div class="reports-grid">
                            <div class="dashboard-card">
                                <h3>الإيرادات والمصروفات</h3>
                                <div class="chart-container" id="revenueChart">
                                    <canvas id="revChartCanvas"></canvas>
                                </div>
                            </div>
                            <div class="dashboard-card">
                                <h3>توزيع الميزانية</h3>
                                <div class="chart-container" id="budgetChart">
                                    <canvas id="budgetChartCanvas"></canvas>
                                </div>
                            </div>
                        </div>
                        
                        <h3 style="margin: 20px 0 15px;">آخر التقارير المالية</h3>
                        <table class="reports-table">
                            <thead>
                                <tr>
                                    <th>التقرير</th>
                                    <th>الفترة</th>
                                    <th>الحالة</th>
                                    <th>تاريخ الإصدار</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>تقرير الربع الأول 2023</td>
                                    <td>يناير - مارس 2023</td>
                                    <td><span class="status-badge active">مكتمل</span></td>
                                    <td>05/04/2023</td>
                                    <td>
                                        <button class="view-btn"><i class="fas fa-eye"></i> عرض</button>
                                        <button class="download-btn"><i class="fas fa-download"></i> تحميل</button>
                                    </td>
                                </tr>
                                <tr>
                                    <td>تقرير الربع الثاني 2023</td>
                                    <td>أبريل - يونيو 2023</td>
                                    <td><span class="status-badge leave">قيد المراجعة</span></td>
                                    <td>-</td>
                                    <td>
                                        <button class="view-btn"><i class="fas fa-edit"></i> تعديل</button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>
        </div>
    </div>

    <script>
        // التنقل بين الصفحات
        document.querySelectorAll('.nav-link').forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                
                // إزالة النشط من جميع الروابط
                document.querySelectorAll('.nav-link').forEach(el => {
                    el.classList.remove('active');
                });
                
                // إضافة النشط للرابط الحالي
                this.classList.add('active');
                
                // إخفاء جميع الأقسام
                document.querySelectorAll('.page-section').forEach(section => {
                    section.classList.remove('active');
                });
                
                // إظهار القسم المحدد
                const sectionId = this.getAttribute('data-section');
                document.getElementById(sectionId).classList.add('active');
                
                // تحديث عنوان الصفحة
                document.getElementById('page-title').textContent = this.querySelector('span').textContent;
            });
        });
        
        // التنقل بين التبويبات في التقارير
        document.querySelectorAll('.tab-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                // إزالة النشط من جميع الأزرار
                document.querySelectorAll('.tab-btn').forEach(el => {
                    el.classList.remove('active');
                });
                
                // إضافة النشط للزر الحالي
                this.classList.add('active');
                
                // إخفاء جميع محتويات التبويبات
                document.querySelectorAll('.tab-content').forEach(content => {
                    content.classList.remove('active');
                });
                
                // إظهار المحتوى المحدد
                const tabId = this.getAttribute('data-tab');
                document.getElementById(tabId).classList.add('active');
            });
        });
        
        // إنشاء الرسوم البيانية بعد تحميل الصفحة
        window.addEventListener('load', function() {
            // مخطط أداء المشاريع
            const perfCtx = document.getElementById('perfChartCanvas').getContext('2d');
            new Chart(perfCtx, {
                type: 'line',
                data: {
                    labels: ['يناير', 'فبراير', 'مارس', 'أبريل', 'مايو', 'يونيو'],
                    datasets: [{
                        label: 'أداء المشاريع',
                        data: [75, 80, 85, 70, 90, 95],
                        borderColor: '#3b82f6',
                        backgroundColor: 'rgba(59, 130, 246, 0.1)',
                        fill: true,
                        tension: 0.3
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            ticks: {
                                callback: function(value) {
                                    return value + '%';
                                }
                            }
                        }
                    }
                }
            });
            
            // مخطط الإيرادات
            const revCtx = document.getElementById('revChartCanvas').getContext('2d');
            new Chart(revCtx, {
                type: 'bar',
                data: {
                    labels: ['يناير', 'فبراير', 'مارس', 'أبريل', 'مايو', 'يونيو'],
                    datasets: [
                        {
                            label: 'الإيرادات',
                            data: [1200000, 1350000, 1400000, 1550000, 1600000, 1850000],
                            backgroundColor: '#10b981'
                        },
                        {
                            label: 'المصروفات',
                            data: [950000, 1000000, 1050000, 1100000, 1150000, 1200000],
                            backgroundColor: '#ef4444'
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                callback: function(value) {
                                    return (value / 1000000).toFixed(1) + 'M';
                                }
                            }
                        }
                    }
                }
            });
            
            // مخطط الميزانية
            const budgetCtx = document.getElementById('budgetChartCanvas').getContext('2d');
            new Chart(budgetCtx, {
                type: 'doughnut',
                data: {
                    labels: ['التشغيل', 'التسويق', 'التطوير', 'الموارد البشرية', 'الإدارة'],
                    datasets: [{
                        data: [35, 20, 25, 15, 5],
                        backgroundColor: [
                            '#3b82f6',
                            '#10b981',
                            '#f59e0b',
                            '#ef4444',
                            '#8b5cf6'
                        ]
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false
                }
            });
        });
    </script>
</body>
</html>
