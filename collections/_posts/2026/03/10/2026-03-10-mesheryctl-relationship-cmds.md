---
title: "mesheryctl relationship commands explained"
subheading: "How to list, search, view, and generate relationship documentation using mesheryctl"
date: 2026-03-10
author: Matthieu Evrin
categories:
  - mesheryctl
featured-image: /assets/images/posts/2026/mesheryctl-relationship/mesheryctl-relationship-cmds.png
redirect_from: /blog/mesheryctl-relationship-commands-explained
published: true
---

If you are managing cloud-native infrastructure with Meshery, understanding how your components interact is critical. This post walks you through the `mesheryctl relationship` commands so you can explore, search, and document relationships directly from your terminal.

> **What is a Meshery Relationship?**  
> In the Meshery ecosystem, a **relationship** defines how two or more [components](https://docs.meshery.io/concepts/logical/components) are interconnected. Relationships capture the dependencies, policies, and interactions between components within a [model](https://docs.meshery.io/concepts/logical/models). They are organized by **kind** (e.g., `hierarchical`, `edge`), **type**, and **subtype** (e.g., `parent`, `binding`) and are evaluated by Meshery's policy engine to enforce design constraints and visualize architectural intent.  
> [Learn more about Meshery Relationships](https://docs.meshery.io/concepts/logical/relationships)

The `mesheryctl relationship` command gives you a convenient CLI interface to interact with the relationships registered in your Meshery Server. It exposes four subcommands — `list`, `search`, `view`, and `generate` — each targeting a specific use case.

---

## Base command: `mesheryctl relationship`

**Description:** The root command for managing relationships. On its own, it prints usage information. Combined with the `--count` flag, it returns the total number of relationships registered in Meshery Server.

**Flags:**

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| `--count` | `-c` | `false` | Get the total number of relationships |
| `--help` | `-h` | | Display help for the command |

**Example — display the total count of registered relationships:**

```shell
$ mesheryctl relationship --count
```

**Example output:**

```
<!-- example output to be added manually -->
```

---

## `mesheryctl relationship list`

**Description:** Lists all relationships registered in Meshery Server, displaying their ID, kind, API version, model name, subtype, and type in a tabular format. Supports paginated output so you can navigate through large sets of results interactively.

**Flags:**

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| `--page` | `-p` | `1` | List next set of relationships at the specified page number |
| `--pagesize` | | `10` | Number of results per page |
| `--count` | `-c` | `false` | Display the total count of relationships only |
| `--help` | `-h` | | Display help for the command |

**Example — list all relationships (page 1, 10 results):**

```shell
$ mesheryctl relationship list
```

**Example output:**

```
<!-- example output to be added manually -->
```

**Additional usage examples:**

```shell
# List relationships on a specific page
mesheryctl relationship list --page 2

# List relationships with a custom page size
mesheryctl relationship list --pagesize 25

# Display only the total count of relationships
mesheryctl relationship list --count
```

---

## `mesheryctl relationship search`

**Description:** Searches registered relationships used by different models. You can narrow down results by kind, type, subtype, and/or model name. At least one filter flag is required.

**Flags:**

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| `--kind` | `-k` | | Search relationships of a particular kind (e.g., `hierarchical`, `edge`) |
| `--type` | `-t` | | Search relationships of a particular type |
| `--subtype` | `-s` | | Search relationships of a particular subtype (e.g., `parent`, `binding`) |
| `--model` | `-m` | | Search relationships belonging to a particular model |
| `--page` | `-p` | `1` | Page number of results to fetch |
| `--help` | `-h` | | Display help for the command |

**Example — search for hierarchical relationships:**

```shell
$ mesheryctl relationship search --kind hierarchical
```

**Example output:**

```
<!-- example output to be added manually -->
```

**Additional usage examples:**

```shell
# Search by subtype
mesheryctl relationship search --subtype parent

# Search by model and kind
mesheryctl relationship search --model kubernetes --kind edge

# Search with pagination
mesheryctl relationship search --type binding --page 2
```

---

## `mesheryctl relationship view`

**Description:** Views the full definition of a specific relationship belonging to a given model. The command fetches the relationships registered for the model you specify, then presents an interactive selection prompt so you can pick the exact relationship you want to inspect. The output is rendered in YAML format by default, or in JSON if requested. You can also save the output to a file.

**Flags:**

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| `--output-format` | `-o` | `yaml` | Format to display in: `json` or `yaml` |
| `--save` | `-s` | `false` | Save the output as a JSON or YAML file |
| `--help` | `-h` | | Display help for the command |

**Example — view relationships of the `kubernetes` model:**

```shell
$ mesheryctl relationship view kubernetes
```

**Example output:**

```
<!-- example output to be added manually -->
```

**Additional usage examples:**

```shell
# View relationships in JSON format
mesheryctl relationship view kubernetes --output-format json

# View relationships and save the output to a file
mesheryctl relationship view kubernetes --output-format json --save
```

---

## `mesheryctl relationship generate`

**Description:** Generates a relationships documentation file (JSON format) by reading data from a Google Spreadsheet. This is primarily a maintainer-facing command used to keep the Meshery documentation up to date with the latest relationship definitions. It requires a valid spreadsheet ID and base64-encoded Google API credentials.

**Flags:**

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| `--spreadsheet-id` | | | *(Required)* Google Spreadsheet ID containing relationship data |
| `--spreadsheet-cred` | | | *(Required)* Base64-encoded Google API credentials |
| `--help` | `-h` | | Display help for the command |

**Example — generate relationship documentation from a spreadsheet:**

```shell
$ mesheryctl relationship generate \
    --spreadsheet-id <your-spreadsheet-id> \
    --spreadsheet-cred $CRED
```

**Example output:**

```
<!-- example output to be added manually -->
```

---

## Conclusion

The `mesheryctl relationship` commands give you direct CLI access to the relationship layer of the Meshery model ecosystem. Whether you want a quick count of registered relationships, need to search for a specific kind, want to inspect a full relationship definition, or are maintaining the documentation data, there is a subcommand for every need.

As a next step, try combining `search` and `view` together: use `search` to find a relationship relevant to your model, then use `view` to inspect its full definition and save it locally for reference.

For more details on how relationships work under the hood, visit the official documentation:

- [Meshery Relationships concept](https://docs.meshery.io/concepts/logical/relationships)
- [mesheryctl relationship CLI reference](https://docs.meshery.io/reference/mesheryctl/relationship)
