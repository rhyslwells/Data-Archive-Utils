# Notes Categorization & Organization Utilities

This utility contains two main functions for managing your markdown notes with YAML frontmatter:

1. **`apply_priority_mapping`** — Assign categories to notes based on tags and a priority order.
2. **`move_notes_by_category`** — Move notes into subfolders according to their category.

---

## 1. `apply_priority_mapping`

### Purpose

Automatically assign a `category` to each note based on its `tags`. Supports:

* Multiple tags per note.
* Priority-based tag matching (first matching tag wins).
* Assigning `"NONE"` if no tags exist.
* Optional overwrite of existing categories (`force=True`).

### Function Signature

```python
apply_priority_mapping(folder_path, mapping, priority_order=None, force=False)
```

### Parameters

* `folder_path` (str) — Path to the folder containing notes.
* `mapping` (dict) — Tag → category mapping dictionary.
* `priority_order` (list, optional) — List of tags in priority order. Defaults to the order of `mapping.keys()`.
* `force` (bool, optional) — If True, overwrite existing category. Default: False.

### Example Usage

```python
TAG_TO_CATEGORY = {
    "ml": "DS",
    "statistics": "STATISTICS",
    "database": "DE",
    "software": "CS",
}

PRIORITY_ORDER = ["ml", "statistics", "database", "software"]

apply_priority_mapping(
    folder_path="path/to/notes",
    mapping=TAG_TO_CATEGORY,
    priority_order=PRIORITY_ORDER,
    force=False
)
```

---

## 2. `move_notes_by_category`

### Purpose

Organize notes by moving them into subfolders corresponding to their `category`. Automatically creates subfolders if needed.

### Function Signature

```python
move_notes_by_category(base_folder, category_folder_map)
```

### Parameters

* `base_folder` (str) — Path to the folder containing notes.
* `category_folder_map` (dict) — Category → folder name mapping. Example:

```python
CATEGORY_TO_FOLDER = {
    "DS": "DS",
    "ML": "ML",
    "DE": "Data Engineering",
    "STATISTICS": "Statistics",
    "CS": "CS",
    "LANG": "Languages",
    "DEVOPS": "DevOps",
    "PM": "Project Management",
    "INDUSTRY": "Industry",
    "DATA_ANALYSIS": "Data Analysis",
    "NONE": "Uncategorized"
}
```

### Example Usage

```python
move_notes_by_category("path/to/notes", CATEGORY_TO_FOLDER)
```

---

## Workflow Example

1. **Assign categories based on tags**:

```python
apply_priority_mapping(
    folder_path="notes",
    mapping=TAG_TO_CATEGORY,
    priority_order=PRIORITY_ORDER,
    force=False
)
```

2. **Move notes to folders by category**:

```python
move_notes_by_category("notes", CATEGORY_TO_FOLDER)
```

This results in all notes being categorized and moved into subfolders named according to their category.

