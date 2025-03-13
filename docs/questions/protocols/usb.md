# Perforce Command Cheat Sheet 🚀

This cheat sheet covers **common Perforce commands** for managing files, checking in/out, shelving (stashing), syncing, branching, and resolving conflicts.

---

## 1️⃣ Setup & Configuration

| **Action** | **Command** |
|------------|------------|
| Set Perforce server | `export P4PORT=ssl:perforce.company.com:1666` |
| Set Perforce user | `export P4USER=username` |
| Set workspace (client) | `export P4CLIENT=workspace_name` |
| Login to Perforce | `p4 login` |
| Logout | `p4 logout` |

---

## 2️⃣ Checking Out & Editing Files

| **Action** | **Command** |
|------------|------------|
| Open a file for editing | `p4 edit file.sv` |
| Check out multiple files | `p4 edit file1.sv file2.sv file3.sv` |
| Check out an entire directory | `p4 edit //depot/path/...` |
| Open a file for add (new file) | `p4 add new_file.sv` |
| Open a file for delete | `p4 delete file.sv` |

---

## 3️⃣ Viewing Checked-Out Files

| **Action** | **Command** |
|------------|------------|
| Show all checked-out files in the workspace | `p4 opened` |
| Show checked-out files in a specific changelist | `p4 opened -c <changelist_number>` |
| Show checked-out files by a specific user | `p4 opened -u username` |

---

## 4️⃣ Submitting (Check-in)

| **Action** | **Command** |
|------------|------------|
| Submit a single file | `p4 submit file.sv -d "Commit message"` |
| Submit multiple files | `p4 submit file1.sv file2.sv -d "Commit message"` |
| Submit all checked-out files | `p4 submit -d "Commit message"` |
| Submit a specific changelist | `p4 submit -c <changelist_number>` |

---

## 5️⃣ Reverting Changes (Undo)

| **Action** | **Command** |
|------------|------------|
| Revert a file | `p4 revert file.sv` |
| Revert all changes | `p4 revert //...` |
| Revert a specific changelist | `p4 revert -c <changelist_number>` |

---

## 6️⃣ Shelving (Stashing)

| **Action** | **Command** |
|------------|------------|
| Shelve all open files in a changelist | `p4 shelve -c <changelist_number>` |
| Shelve a specific file | `p4 shelve -c <changelist_number> file.sv` |
| Unshelve files (restore stashed work) | `p4 unshelve -s <changelist_number>` |
| Delete shelved changes | `p4 shelve -d -c <changelist_number>` |

---

## 7️⃣ Syncing Files (Pull from Depot)

| **Action** | **Command** |
|------------|------------|
| Sync all files in the workspace | `p4 sync` |
| Sync a specific file | `p4 sync file.sv` |
| Sync a specific revision | `p4 sync file.sv@12345` |
| Sync a specific changelist | `p4 sync file.sv@<changelist_number>` |

---

## 8️⃣ Comparing Files (Diff)

| **Action** | **Command** |
|------------|------------|
| Compare local file with last synced version | `p4 diff file.sv` |
| Compare local file with a specific revision | `p4 diff file.sv#5` |
| Compare two depot versions | `p4 diff2 file.sv#5 file.sv#10` |
| Open GUI diff tool (P4Merge) | `p4 diff -g file.sv` |

---

## 9️⃣ Viewing File History

| **Action** | **Command** |
|------------|------------|
| Show revision history of a file | `p4 filelog file.sv` |
| Show changes in a file | `p4 changes file.sv` |
| Show details of a specific changelist | `p4 describe <changelist_number>` |
| Show last 10 submitted changes | `p4 changes -m 10` |

---

## 🔟 Branching & Integration

| **Action** | **Command** |
|------------|------------|
| Branch a file | `p4 integrate //depot/main/file.sv //depot/branch/file.sv` |
| Resolve integration conflicts | `p4 resolve` |
| Submit merged changes | `p4 submit` |

---

## 11️⃣ Miscellaneous

| **Action** | **Command** |
|------------|------------|
| List all pending changelists | `p4 changes -s pending` |
| List files in a changelist | `p4 opened -c <changelist_number>` |
| Delete a pending changelist | `p4 change -d <changelist_number>` |
| Change ownership of a changelist | `p4 change -o | p4 change -i` |

---

## 🚀 Best Practices

- Use descriptive changelist messages (`p4 submit -d "Fix CDC issue in file.sv"`).
- Shelve work before switching tasks (`p4 shelve -c 12345`).
- Sync regularly to avoid conflicts (`p4 sync`).
- Use diff tools (`p4 diff` or `p4 diff -g`) to review changes before submission.

---
