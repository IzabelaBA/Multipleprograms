
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Service Tasks - All Programs</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Salesforce Sans', -apple-system, BlinkMacSystemFont, sans-serif;
            background: #f3f3f3;
            color: #181818;
        }

        .salesforce-header {
            background: #1B96FF;
            color: white;
            padding: 0.75rem 1rem;
            display: flex;
            align-items: center;
            gap: 1rem;
            font-size: 0.875rem;
        }

        .sf-logo {
            width: 24px;
            height: 24px;
            background: white;
            border-radius: 3px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #1B96FF;
            font-weight: bold;
        }

        .nav-item {
            color: white;
            text-decoration: none;
            padding: 0.5rem;
            border-radius: 4px;
            transition: background 0.2s ease;
        }

        .nav-item:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        .nav-item.active {
            background: rgba(255, 255, 255, 0.2);
        }

        .main-content {
            padding: 2rem;
        }

        .container {
            max-width: 1600px;
            margin: 0 auto;
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background: #f8f9fa;
            padding: 1.5rem;
            border-bottom: 1px solid #e5e5e5;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .header h1 {
            font-size: 1.25rem;
            font-weight: 600;
            color: #181818;
        }

        .table-container {
            overflow-x: auto;
        }

        .service-table {
            width: 100%;
            border-collapse: collapse;
            background: white;
        }

        .service-table th {
            background: #f8f9fa;
            padding: 0.5rem;
            text-align: left;
            font-weight: 600;
            font-size: 0.875rem;
            color: #3E3E3C;
            border-bottom: 2px solid #e5e5e5;
            white-space: nowrap;
            cursor: pointer;
            position: relative;
            user-select: none;
        }

        .service-table th:hover {
            background: #e9ecef;
        }

        .service-table th.sortable::after {
            content: ' ↕';
            color: #706E6B;
            font-size: 0.75rem;
            margin-left: 0.25rem;
        }

        .service-table th.sort-asc::after {
            content: ' ↑';
            color: #0176D3;
        }

        .service-table th.sort-desc::after {
            content: ' ↓';
            color: #0176D3;
        }

        .service-table td {
            padding: 0.5rem;
            border-bottom: 1px solid #e5e5e5;
            vertical-align: top;
        }

        .service-table tbody tr:hover {
            background: #f8f9fa;
        }

        .task-row {
            transition: background-color 0.2s ease;
        }

        .service-name {
            font-weight: 600;
            color: #0176D3;
            font-size: 0.875rem;
            cursor: pointer;
            text-decoration: underline;
        }

        .service-name:hover {
            color: #014486;
        }

        .program-name, .user-name, .due-date, .status-text {
            font-size: 0.875rem;
            color: #181818;
        }

        .package-text {
            font-size: 0.875rem;
            color: #181818;
        }

        /* Modal Styles */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
        }

        .modal {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            border-radius: 8px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2);
            width: 600px;
            max-width: 90vw;
            z-index: 1001;
        }

        .modal-header {
            padding: 1.5rem;
            border-bottom: 1px solid #e5e5e5;
            background: #f8f9fa;
            border-radius: 8px 8px 0 0;
            position: relative;
        }

        .modal-title {
            font-size: 1.25rem;
            font-weight: 600;
            color: #181818;
            margin: 0;
        }

        .modal-body {
            padding: 1.5rem;
        }

        .detail-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1.5rem;
            margin-bottom: 1.5rem;
        }

        .detail-field {
            margin-bottom: 1rem;
        }

        .detail-field.full-width {
            grid-column: 1 / -1;
        }

        .detail-label {
            display: block;
            font-weight: 600;
            color: #3E3E3C;
            font-size: 0.875rem;
            margin-bottom: 0.5rem;
        }

        .detail-input, .detail-select, .detail-textarea {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #D8D8D8;
            border-radius: 4px;
            font-size: 0.875rem;
            background: white;
        }

        .detail-input:focus, .detail-select:focus, .detail-textarea:focus {
            outline: none;
            border-color: #0176D3;
            box-shadow: 0 0 0 2px rgba(1, 118, 211, 0.1);
        }

        .detail-textarea {
            min-height: 100px;
            resize: vertical;
            font-family: inherit;
        }

        .close-btn {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: none;
            border: none;
            font-size: 1.5rem;
            color: #706E6B;
            cursor: pointer;
            width: 2rem;
            height: 2rem;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 4px;
        }

        .close-btn:hover {
            background: #f0f0f0;
            color: #181818;
        }

        .modal-actions {
            padding: 1rem 1.5rem;
            border-top: 1px solid #e5e5e5;
            background: #f8f9fa;
            display: flex;
            justify-content: flex-end;
            gap: 0.75rem;
            border-radius: 0 0 8px 8px;
        }

        .btn {
            padding: 0.75rem 1.5rem;
            border-radius: 6px;
            font-weight: 600;
            font-size: 0.875rem;
            cursor: pointer;
            border: none;
            transition: all 0.2s ease;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
        }

        .btn-primary {
            background: #0176D3;
            color: white;
        }

        .btn-primary:hover {
            background: #014486;
        }

        .btn-secondary {
            background: white;
            color: #0176D3;
            border: 1px solid #0176D3;
        }

        .btn-secondary:hover {
            background: #f8f9fa;
        }
    </style>
</head>
<body>
    <!-- Salesforce-style Header -->
    <div class="salesforce-header">
        <div class="sf-logo">☁</div>
        <a href="#" class="nav-item">Accounts</a>
        <a href="#" class="nav-item">Opportunities</a>
        <a href="#" class="nav-item">Contracts</a>
        <a href="#" class="nav-item active">SLA Services</a>
        <a href="#" class="nav-item">My SLA Board</a>
    </div>

    <div class="main-content">
        <div class="container">
            <div class="header">
                <h1>Tasks</h1>
            </div>

            <div class="table-container">
                <table class="service-table">
                    <thead>
                        <tr>
                            <th style="width: 25%;">Service Name</th>
                            <th style="width: 20%;" class="sortable" onclick="sortTable('program')">Program</th>
                            <th style="width: 12%;" class="sortable" onclick="sortTable('package')">Package</th>
                            <th style="width: 12%;" class="sortable" onclick="sortTable('dueDate')">Due Date</th>
                            <th style="width: 15%;" class="sortable" onclick="sortTable('assignedTo')">Assigned To</th>
                            <th style="width: 16%;" class="sortable" onclick="sortTable('status')">Status</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Performance Reviews', 'Monthly analysis of campaign performance and optimization recommendations', 'TechCorp Affiliate Program', 'Premium', '2025-06-15', 'Chandler Bing', 'Monthly performance analysis completed', 'completed')">
                                    Performance Reviews
                                </div>
                            </td>
                            <td><div class="program-name">TechCorp Affiliate Program</div></td>
                            <td><div class="package-text">Premium</div></td>
                            <td><div class="due-date">2025-06-15</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text">Completed</div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Publisher Recommendations', 'Monthly publisher outreach and partnership recommendations', 'TechCorp Affiliate Program', 'Premium', '2025-06-20', 'Chandler Bing', 'Research new tech publishers for Q3 campaign', 'empty')">
                                    Publisher Recommendations
                                </div>
                            </td>
                            <td><div class="program-name">TechCorp Affiliate Program</div></td>
                            <td><div class="package-text">Premium</div></td>
                            <td><div class="due-date">2025-06-20</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text"></div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Monthly Check-ins', 'Regular client communication and strategy discussion', 'TechCorp Affiliate Program', 'Premium', '2025-06-10', 'Chandler Bing', 'Client very satisfied with current performance', 'completed')">
                                    Monthly Check-ins
                                </div>
                            </td>
                            <td><div class="program-name">TechCorp Affiliate Program</div></td>
                            <td><div class="package-text">Premium</div></td>
                            <td><div class="due-date">2025-06-10</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text">Completed</div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Account Maintenance', 'Regular account cleanup and maintenance tasks', 'TechCorp Affiliate Program', 'Premium', '2025-06-25', 'Chandler Bing', 'Scheduled maintenance for inactive publishers', 'empty')">
                                    Account Maintenance
                                </div>
                            </td>
                            <td><div class="program-name">TechCorp Affiliate Program</div></td>
                            <td><div class="package-text">Premium</div></td>
                            <td><div class="due-date">2025-06-25</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text"></div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Business Review', 'Quarterly business performance review and strategic assessment', 'Healthcare Partners', 'Core', '2025-07-01', 'Chandler Bing', 'Q2 review shows strong growth in health sector', 'completed')">
                                    Business Review
                                </div>
                            </td>
                            <td><div class="program-name">Healthcare Partners</div></td>
                            <td><div class="package-text">Core</div></td>
                            <td><div class="due-date">2025-07-01</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text">Completed</div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Campaign Analysis', 'Detailed campaign performance analysis and recommendations', 'Fashion Forward Partners', 'Premium', '2025-06-18', 'Chandler Bing', 'Analyzing fashion trends and conversion rates', 'empty')">
                                    Campaign Analysis
                                </div>
                            </td>
                            <td><div class="program-name">Fashion Forward Partners</div></td>
                            <td><div class="package-text">Premium</div></td>
                            <td><div class="due-date">2025-06-18</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text"></div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Publisher Approvals', 'Weekly publisher approval and onboarding process', 'Travel Deals Program', 'Essential', '2025-06-22', 'Chandler Bing', 'Reviewing travel publisher applications', 'skipped')">
                                    Publisher Approvals
                                </div>
                            </td>
                            <td><div class="program-name">Travel Deals Program</div></td>
                            <td><div class="package-text">Essential</div></td>
                            <td><div class="due-date">2025-06-22</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text">Skipped</div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Competitor Analysis', 'Monthly competitor benchmarking and market analysis', 'Software Solutions Affiliate', 'Premium', '2025-06-28', 'Chandler Bing', 'Analyzing competitor pricing strategies', 'empty')">
                                    Competitor Analysis
                                </div>
                            </td>
                            <td><div class="program-name">Software Solutions Affiliate</div></td>
                            <td><div class="package-text">Premium</div></td>
                            <td><div class="due-date">2025-06-28</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text"></div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Strategy Planning', 'Quarterly strategic planning and roadmap development', 'FinTech Solutions', 'Premium', '2025-07-05', 'Chandler Bing', 'Developing Q3 growth strategy', 'empty')">
                                    Strategy Planning
                                </div>
                            </td>
                            <td><div class="program-name">FinTech Solutions</div></td>
                            <td><div class="package-text">Premium</div></td>
                            <td><div class="due-date">2025-07-05</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text"></div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Content Review', 'Monthly content and creative asset review', 'E-commerce Electronics', 'Core', '2025-06-30', 'Chandler Bing', 'Reviewing product descriptions and images', 'completed')">
                                    Content Review
                                </div>
                            </td>
                            <td><div class="program-name">E-commerce Electronics</div></td>
                            <td><div class="package-text">Core</div></td>
                            <td><div class="due-date">2025-06-30</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text">Completed</div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Network Growth', 'Weekly publisher recruitment and network expansion', 'Home & Garden Network', 'Essential', '2025-07-03', 'Chandler Bing', 'Identifying new home improvement publishers', 'empty')">
                                    Network Growth
                                </div>
                            </td>
                            <td><div class="program-name">Home & Garden Network</div></td>
                            <td><div class="package-text">Essential</div></td>
                            <td><div class="due-date">2025-07-03</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text"></div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Technical Integration', 'API integration and technical setup support', 'Automotive Parts Hub', 'Premium', '2025-07-08', 'Chandler Bing', 'Setting up tracking integration', 'empty')">
                                    Technical Integration
                                </div>
                            </td>
                            <td><div class="program-name">Automotive Parts Hub</div></td>
                            <td><div class="package-text">Premium</div></td>
                            <td><div class="due-date">2025-07-08</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text"></div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Fraud Monitoring', 'Weekly fraud detection and prevention review', 'Financial Services Pro', 'Core', '2025-06-26', 'Chandler Bing', 'Monitoring suspicious transaction patterns', 'completed')">
                                    Fraud Monitoring
                                </div>
                            </td>
                            <td><div class="program-name">Financial Services Pro</div></td>
                            <td><div class="package-text">Core</div></td>
                            <td><div class="due-date">2025-06-26</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text">Completed</div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Training & Support', 'Monthly publisher training and support sessions', 'Education Platform', 'Essential', '2025-07-10', 'Chandler Bing', 'Preparing training materials for new publishers', 'empty')">
                                    Training & Support
                                </div>
                            </td>
                            <td><div class="program-name">Education Platform</div></td>
                            <td><div class="package-text">Essential</div></td>
                            <td><div class="due-date">2025-07-10</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text"></div></td>
                        </tr>
                        <tr class="task-row">
                            <td>
                                <div class="service-name" onclick="openTaskDetail('Compliance Audit', 'Quarterly compliance and regulatory review', 'Insurance Solutions', 'Premium', '2025-07-12', 'Chandler Bing', 'Reviewing GDPR and privacy compliance', 'skipped')">
                                    Compliance Audit
                                </div>
                            </td>
                            <td><div class="program-name">Insurance Solutions</div></td>
                            <td><div class="package-text">Premium</div></td>
                            <td><div class="due-date">2025-07-12</div></td>
                            <td><div class="user-name">Chandler Bing</div></td>
                            <td><div class="status-text">Skipped</div></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- Task Detail Modal -->
    <div id="taskDetailModal" class="modal-overlay">
        <div class="modal">
            <div class="modal-header">
                <h2 class="modal-title" id="taskDetailTitle">Task Details</h2>
                <button class="close-btn" id="closeTaskDetailBtn">&times;</button>
            </div>
            <div class="modal-body">
                <div class="detail-grid">
                    <div class="detail-field">
                        <label class="detail-label">Program Name</label>
                        <input type="text" id="taskDetailProgram" class="detail-input" readonly>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Package</label>
                        <input type="text" id="taskDetailPackage" class="detail-input" readonly>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Service Name</label>
                        <input type="text" id="taskDetailName" class="detail-input" readonly>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Category</label>
                        <input type="text" id="taskDetailCategory" class="detail-input" value="Service Management" readonly>
                    </div>
                    <div class="detail-field full-width">
                        <label class="detail-label">Service Description</label>
                        <textarea id="taskDetailDescription" class="detail-textarea" readonly></textarea>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Due Date</label>
                        <input type="date" id="taskDetailDueDate" class="detail-input">
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Assigned To</label>
                        <select id="taskDetailAssigned" class="detail-select">
                            <option>Chandler Bing</option>
                            <option>Monica Geller</option>
                            <option>Ross Geller</option>
                            <option>Rachel Green</option>
                            <option>Joey Tribbiani</option>
                            <option>Phoebe Buffay</option>
                            <option>Cristina</option>
                        </select>
                    </div>
                    <div class="detail-field">
                        <label class="detail-label">Status</label>
                        <select id="taskDetailStatus" class="detail-select">
                            <option value="empty">Empty</option>
                            <option value="completed">Completed</option>
                            <option value="skipped">Skipped</option>
                        </select>
                    </div>
                    <div class="detail-field full-width">
                        <label class="detail-label">Notes</label>
                        <textarea id="taskDetailNotes" class="detail-textarea" placeholder="Add notes, comments, or updates about this task..."></textarea>
                    </div>
                </div>
            </div>
            <div class="modal-actions">
                <button class="btn btn-secondary" id="cancelTaskDetailBtn">Cancel</button>
                <button class="btn btn-primary" id="saveTaskDetailBtn">Save Changes</button>
            </div>
        </div>
    </div>

    <script>
        let currentTaskData = {};
        let currentSort = { column: null, direction: 'asc' };

        // Store all table data for sorting
        let tableData = [
            {
                serviceName: 'Performance Reviews',
                program: 'TechCorp Affiliate Program',
                package: 'Premium',
                dueDate: '2025-06-15',
                assignedTo: 'Chandler Bing',
                status: 'Completed',
                description: 'Monthly analysis of campaign performance and optimization recommendations',
                notes: 'Monthly performance analysis completed',
                statusValue: 'completed'
            },
            {
                serviceName: 'Publisher Recommendations',
                program: 'TechCorp Affiliate Program',
                package: 'Premium',
                dueDate: '2025-06-20',
                assignedTo: 'Chandler Bing',
                status: '',
                description: 'Monthly publisher outreach and partnership recommendations',
                notes: 'Research new tech publishers for Q3 campaign',
                statusValue: 'empty'
            },
            {
                serviceName: 'Monthly Check-ins',
                program: 'TechCorp Affiliate Program',
                package: 'Premium',
                dueDate: '2025-06-10',
                assignedTo: 'Chandler Bing',
                status: 'Completed',
                description: 'Regular client communication and strategy discussion',
                notes: 'Client very satisfied with current performance',
                statusValue: 'completed'
            },
            {
                serviceName: 'Account Maintenance',
                program: 'TechCorp Affiliate Program',
                package: 'Premium',
                dueDate: '2025-06-25',
                assignedTo: 'Chandler Bing',
                status: '',
                description: 'Regular account cleanup and maintenance tasks',
                notes: 'Scheduled maintenance for inactive publishers',
                statusValue: 'empty'
            },
            {
                serviceName: 'Business Review',
                program: 'Healthcare Partners',
                package: 'Core',
                dueDate: '2025-07-01',
                assignedTo: 'Chandler Bing',
                status: 'Completed',
                description: 'Quarterly business performance review and strategic assessment',
                notes: 'Q2 review shows strong growth in health sector',
                statusValue: 'completed'
            },
            {
                serviceName: 'Campaign Analysis',
                program: 'Fashion Forward Partners',
                package: 'Premium',
                dueDate: '2025-06-18',
                assignedTo: 'Chandler Bing',
                status: '',
                description: 'Detailed campaign performance analysis and recommendations',
                notes: 'Analyzing fashion trends and conversion rates',
                statusValue: 'empty'
            },
            {
                serviceName: 'Publisher Approvals',
                program: 'Travel Deals Program',
                package: 'Essential',
                dueDate: '2025-06-22',
                assignedTo: 'Chandler Bing',
                status: 'Skipped',
                description: 'Weekly publisher approval and onboarding process',
                notes: 'Reviewing travel publisher applications',
                statusValue: 'skipped'
            },
            {
                serviceName: 'Competitor Analysis',
                program: 'Software Solutions Affiliate',
                package: 'Premium',
                dueDate: '2025-06-28',
                assignedTo: 'Chandler Bing',
                status: '',
                description: 'Monthly competitor benchmarking and market analysis',
                notes: 'Analyzing competitor pricing strategies',
                statusValue: 'empty'
            },
            {
                serviceName: 'Strategy Planning',
                program: 'FinTech Solutions',
                package: 'Premium',
                dueDate: '2025-07-05',
                assignedTo: 'Chandler Bing',
                status: '',
                description: 'Quarterly strategic planning and roadmap development',
                notes: 'Developing Q3 growth strategy',
                statusValue: 'empty'
            },
            {
                serviceName: 'Content Review',
                program: 'E-commerce Electronics',
                package: 'Core',
                dueDate: '2025-06-30',
                assignedTo: 'Chandler Bing',
                status: 'Completed',
                description: 'Monthly content and creative asset review',
                notes: 'Reviewing product descriptions and images',
                statusValue: 'completed'
            },
            {
                serviceName: 'Network Growth',
                program: 'Home & Garden Network',
                package: 'Essential',
                dueDate: '2025-07-03',
                assignedTo: 'Chandler Bing',
                status: '',
                description: 'Weekly publisher recruitment and network expansion',
                notes: 'Identifying new home improvement publishers',
                statusValue: 'empty'
            },
            {
                serviceName: 'Technical Integration',
                program: 'Automotive Parts Hub',
                package: 'Premium',
                dueDate: '2025-07-08',
                assignedTo: 'Chandler Bing',
                status: '',
                description: 'API integration and technical setup support',
                notes: 'Setting up tracking integration',
                statusValue: 'empty'
            },
            {
                serviceName: 'Fraud Monitoring',
                program: 'Financial Services Pro',
                package: 'Core',
                dueDate: '2025-06-26',
                assignedTo: 'Chandler Bing',
                status: 'Completed',
                description: 'Weekly fraud detection and prevention review',
                notes: 'Monitoring suspicious transaction patterns',
                statusValue: 'completed'
            },
            {
                serviceName: 'Training & Support',
                program: 'Education Platform',
                package: 'Essential',
                dueDate: '2025-07-10',
                assignedTo: 'Chandler Bing',
                status: '',
                description: 'Monthly publisher training and support sessions',
                notes: 'Preparing training materials for new publishers',
                statusValue: 'empty'
            },
            {
                serviceName: 'Compliance Audit',
                program: 'Insurance Solutions',
                package: 'Premium',
                dueDate: '2025-07-12',
                assignedTo: 'Chandler Bing',
                status: 'Skipped',
                description: 'Quarterly compliance and regulatory review',
                notes: 'Reviewing GDPR and privacy compliance',
                statusValue: 'skipped'
            }
        ];

        document.addEventListener('DOMContentLoaded', function() {
            initializeModals();
        });

        function sortTable(column) {
            if (currentSort.column === column) {
                currentSort.direction = currentSort.direction === 'asc' ? 'desc' : 'asc';
            } else {
                currentSort.column = column;
                currentSort.direction = 'asc';
            }

            updateSortHeaders();

            // Sort the data
            tableData.sort((a, b) => {
                let valueA, valueB;

                switch(column) {
                    case 'program':
                        valueA = a.program;
                        valueB = b.program;
                        break;
                    case 'package':
                        valueA = a.package;
                        valueB = b.package;
                        break;
                    case 'dueDate':
                        valueA = new Date(a.dueDate);
                        valueB = new Date(b.dueDate);
                        break;
                    case 'assignedTo':
                        valueA = a.assignedTo;
                        valueB = b.assignedTo;
                        break;
                    case 'status':
                        const statusOrder = { 'completed': 1, 'skipped': 2, 'empty': 3 };
                        valueA = statusOrder[a.statusValue] || 3;
                        valueB = statusOrder[b.statusValue] || 3;
                        break;
                    default:
                        return 0;
                }

                if (column === 'dueDate') {
                    return currentSort.direction === 'asc' ? valueA - valueB : valueB - valueA;
                } else if (column === 'status') {
                    return currentSort.direction === 'asc' ? valueA - valueB : valueB - valueA;
                } else {
                    if (valueA < valueB) return currentSort.direction === 'asc' ? -1 : 1;
                    if (valueA > valueB) return currentSort.direction === 'asc' ? 1 : -1;
                    return 0;
                }
            });

            renderTable();
        }

        function updateSortHeaders() {
            const headers = document.querySelectorAll('.sortable');
            headers.forEach(header => {
                header.classList.remove('sort-asc', 'sort-desc');
            });

            const currentHeader = document.querySelector(`[onclick="sortTable('${currentSort.column}')"]`);
            if (currentHeader) {
                currentHeader.classList.add(currentSort.direction === 'asc' ? 'sort-asc' : 'sort-desc');
            }
        }

        function renderTable() {
            const tbody = document.querySelector('.service-table tbody');
            tbody.innerHTML = '';

            tableData.forEach(row => {
                const tr = document.createElement('tr');
                tr.className = 'task-row';
                tr.innerHTML = `
                    <td>
                        <div class="service-name" onclick="openTaskDetail('${row.serviceName}', '${row.description}', '${row.program}', '${row.package}', '${row.dueDate}', '${row.assignedTo}', '${row.notes}', '${row.statusValue}')">
                            ${row.serviceName}
                        </div>
                    </td>
                    <td><div class="program-name">${row.program}</div></td>
                    <td><div class="package-text">${row.package}</div></td>
                    <td><div class="due-date">${row.dueDate}</div></td>
                    <td><div class="user-name">${row.assignedTo}</div></td>
                    <td><div class="status-text">${row.status}</div></td>
                `;
                tbody.appendChild(tr);
            });
        }

        function initializeModals() {
            const taskDetailModal = document.getElementById('taskDetailModal');
            const closeTaskDetailBtn = document.getElementById('closeTaskDetailBtn');
            const cancelTaskDetailBtn = document.getElementById('cancelTaskDetailBtn');
            const saveTaskDetailBtn = document.getElementById('saveTaskDetailBtn');

            if (closeTaskDetailBtn) {
                closeTaskDetailBtn.addEventListener('click', () => {
                    taskDetailModal.style.display = 'none';
                });
            }

            if (cancelTaskDetailBtn) {
                cancelTaskDetailBtn.addEventListener('click', () => {
                    taskDetailModal.style.display = 'none';
                });
            }

            if (saveTaskDetailBtn) {
                saveTaskDetailBtn.addEventListener('click', () => {
                    saveTaskDetails();
                });
            }

            window.addEventListener('click', (e) => {
                if (e.target === taskDetailModal) {
                    taskDetailModal.style.display = 'none';
                }
            });
        }

        function openTaskDetail(name, description, program, packageType, dueDate, assignedTo, notes, status) {
            currentTaskData = {
                name: name,
                description: description,
                program: program,
                packageType: packageType,
                dueDate: dueDate,
                assignedTo: assignedTo,
                notes: notes,
                status: status
            };

            document.getElementById('taskDetailTitle').textContent = name;
            document.getElementById('taskDetailProgram').value = program;
            document.getElementById('taskDetailPackage').value = packageType;
            document.getElementById('taskDetailName').value = name;
            document.getElementById('taskDetailDescription').value = description;
            document.getElementById('taskDetailDueDate').value = dueDate;
            document.getElementById('taskDetailNotes').value = notes;
            
            const assignedSelect = document.getElementById('taskDetailAssigned');
            if (assignedSelect) {
                assignedSelect.value = assignedTo;
            }

            const statusSelect = document.getElementById('taskDetailStatus');
            if (statusSelect) {
                statusSelect.value = status;
            }

            document.getElementById('taskDetailModal').style.display = 'block';
        }

        function saveTaskDetails() {
            const updatedData = {
                name: document.getElementById('taskDetailName').value,
                description: document.getElementById('taskDetailDescription').value,
                program: document.getElementById('taskDetailProgram').value,
                packageType: document.getElementById('taskDetailPackage').value,
                dueDate: document.getElementById('taskDetailDueDate').value,
                assignedTo: document.getElementById('taskDetailAssigned').value,
                notes: document.getElementById('taskDetailNotes').value,
                status: document.getElementById('taskDetailStatus').value
            };

            // Update the data in tableData array
            const dataIndex = tableData.findIndex(item => 
                item.serviceName === currentTaskData.name && 
                item.program === currentTaskData.program
            );

            if (dataIndex !== -1) {
                tableData[dataIndex].dueDate = updatedData.dueDate;
                tableData[dataIndex].assignedTo = updatedData.assignedTo;
                tableData[dataIndex].notes = updatedData.notes;
                tableData[dataIndex].statusValue = updatedData.status;
                
                // Update status display text
                switch(updatedData.status) {
                    case 'completed':
                        tableData[dataIndex].status = 'Completed';
                        break;
                    case 'skipped':
                        tableData[dataIndex].status = 'Skipped';
                        break;
                    default:
                        tableData[dataIndex].status = '';
                }

                // Re-render the table to reflect changes
                renderTable();
            }

            alert('Task details saved successfully!');
            document.getElementById('taskDetailModal').style.display = 'none';
        }
    </script>
</body>
</html>

