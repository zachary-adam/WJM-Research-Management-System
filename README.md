# Wisdom Journal Manager

**A full-stack WordPress solution for managing academic journals, issues, papers, and authors with automated citation tracking and enterprise-grade security.**

[![WordPress](https://img.shields.io/badge/WordPress-5.0+-21759b.svg?style=flat-square)](https://wordpress.org)
[![PHP](https://img.shields.io/badge/PHP-7.4+-777bb4.svg?style=flat-square)](https://php.net)
[![License](https://img.shields.io/badge/License-GPL--v2-green.svg?style=flat-square)](https://www.gnu.org/licenses/gpl-2.0.html)
[![Stable](https://img.shields.io/badge/Stable-1.0.0-blue.svg?style=flat-square)](#)

Developed by **Aethex**, Wisdom Journal Manager provides a comprehensive infrastructure for academic publishing. The platform manages the complete publication hierarchy—Journals, Issues, Papers, and Authors—integrating professional editorial workflows with robust automation and security.

---

## Publication Hierarchy

The system architecture is built on a structured relational model to ensure data integrity and academic compliance:

* **Journals:** Top-level containers supporting ISSN, publisher details, editorial board management, and unique branding.
* **Issues:** Publication units linked to specific journals, supporting volume/numbering, special issues, and guest editors.
* **Papers:** Scholarly items featuring DOI integration, versioning history, open access flags, and compliance metadata.
* **Authors:** Dedicated records stored in the custom `wp_sjm_authors` table, featuring ORCID integration and cross-linked attribution.

---

## Functional Modules

### Administrative Management
* **Editorial Workflow:** Assign roles including Editor-in-Chief, Managing Editor, Reviewers, and Layout Editors per journal or issue.
* **Lifecycle Tracking:** Monitor paper status with comprehensive timestamps, editorial notes, and tracking history.
* **Compliance & Rights:** Dedicated fields for funding statements, conflicts of interest, ethics committee approval, and data availability.
* **Versioning System:** Sophisticated version control allowing for multiple revisions, types (Preprint/Final), and public history displays.

### Automation & API Integrations
The plugin features a robust engine to maintain real-time citation metrics and scholarly data:
* **Standard Integrations:** CrossRef (DOI), Semantic Scholar, and arXiv.
* **Enterprise Integrations:** Scopus and Web of Science (requires valid API credentials).
* **Security:** All external API keys are stored at rest using **AES-256-CBC encryption** derived from WordPress security salts.

### Security & Data Integrity
* **Role-Based Access Control:** Granular capability checks enforced across all administrative actions.
* **Rate Limiting:** Sophisticated quotas to prevent API abuse and ensure server stability.
* **Audit Logging:** A centralized security log records severity levels, IP addresses, and user contexts for all critical events.
* **SQL Safety:** Full implementation of parameterized queries and CSRF protection via WordPress nonces.

---

## Shortcode Reference

Standardized shortcodes allow for the deployment of academic content across any WordPress page or post.

| Shortcode | Parameters | Description |
| :--- | :--- | :--- |
| `[journals]` | `layout`, `publisher`, `year` | Renders a grid or list view of available journals. |
| `[issues]` | `journal_id`, `volume`, `special_issue` | Displays issues filtered by journal or specific criteria. |
| `[papers]` | `author`, `keyword`, `paper_type` | Lists papers with advanced metadata filtering options. |
| `[wjm_author_profile]`| `id` | Embeds a specific author profile card with publication history. |

---

## User Roles & System Quotas

To maintain operational performance, the system enforces hourly rate limits for API and data operations.

| User Role | API Calls / hr | Data Fetches / hr | System Permissions |
| :--- | :--- | :--- | :--- |
| **Student** | 50 | 30 | Read-only access. |
| **Researcher** | 100 | 60 | Read access and management of personal papers. |
| **Editor** | 200 | 120 | Full management of journals, issues, and papers. |
| **Administrator**| 500 | 300 | Unrestricted system configuration and security logs. |

---

## Technical Documentation

<details>
<summary>System Requirements & Deployment</summary>

* **Requirements:** WordPress 5.0+, PHP 7.4+, MySQL 5.6+ (or MariaDB equivalent).
* **Required Extensions:** `curl`, `json`.
* **Installation:**
    1. Upload the plugin package to the `/wp-content/plugins/` directory.
    2. Activate the plugin via the WordPress Admin dashboard.
    3. Navigate to **Journals → Plugin Verification** to run the diagnostic suite.
    4. Configure API keys and automation frequency under **Journals → Automation**.
</details>

<details>
<summary>Data Model & Development Hooks</summary>

**Database Architecture:**
The plugin utilizes the standard WordPress post table for hierarchical content and a custom `wp_sjm_authors` table for high-performance author querying.

**Action Hooks:**
* `sjm_after_save_journal`: Fires following journal metadata updates.
* `sjm_after_save_paper`: Fires following paper publication or revision.
* `sjm_security_event_logged`: Triggered when an event is added to the security audit trail.

**Filter Hooks:**
* `sjm_paper_query_args`: Modify the query parameters for paper listing shortcodes.
* `sjm_journal_query_args`: Customize the retrieval of journal objects.
</details>

---

## Frequently Asked Questions

**How is citation data kept current?**
Metrics are updated through a background process (cron) on a daily, weekly, or monthly schedule as configured in the Automation settings. Manual updates are available on a per-paper basis.

**How does the system handle Open Access?**
The system supports both Open Access and Peer-Reviewed flags at the journal and paper levels. These flags automate the display of standard academic badges and metadata on the frontend.

**What happens to data upon plugin deactivation?**
Deactivation preserves all content and settings. Uninstallation via the WordPress dashboard will remove plugin-specific settings and scheduled tasks, but all Journal, Issue, and Paper post types remain in the database for data retention.

---

## Troubleshooting

* **Interface Visibility:** Ensure the user has the appropriate role assigned under **Journals → User Roles**.
* **Metric Sync Failures:** Verify that outbound server requests are permitted and that API rate limits have not been exceeded.
* **Template Styling:** The plugin enqueues specific CSS for academic templates. If theme conflicts occur, use the `.sjm-single-container` class for CSS specificity overrides.

---

## Credits & Licensing

* **Principal Developer:** Zachary Adam
* **Organization:** [Aethex Web Solutions](http://aethexweb.com)
* **Compliance:** Follows WordPress coding standards and security best practices.
* **License:** Distributed under the GNU General Public License v2 or later.

---
*Wisdom Journal Manager — Engineered for Academic Excellence.*