# Node Types

This configuration defines how to deal with different kinds of nodes (files,
directories, symlinks etc.) in a directory.

This can be configured using the `xplr.config.node_types` Lua API.

It contains the following fields:

- [directory][1]
- [file][2]
- [symlink][3]
- [mime_essence][4]
- [extension][5]
- [special][6]

One node can fall into multiple categories. For example, a node can have the
extension `md`, and be a `file`. In that case, the properties from the more
specific category i.e. extension will be used.

The priority is:

**special** > **extension** > **mime_essence** > **symlink** > **file** > **directory**

### directory

Type: [NodeType Config][7]

Properties related to directories are defined here.

Contains the following fields:

Example:

```lua
xplr.config.node_types.directory.meta.icon = ""
xplr.config.node_types.directory.style.add_modifiers = { "Bold" }
```

### file

Type: [NodeType Config][7]

Properties related to regular files are defined here.

Contains the following fields:

Example:

```lua
xplr.config.node_types.file.meta.icon = ""
xplr.config.node_types.file.style.fg = "White"
```

### symlink

Type: [NodeType Config][7]

Properties related to symlink are defined here.

Example:

```lua
xplr.config.node_types.symlink.meta.icon = ""
xplr.config.node_types.symlink.style.add_modifiers = { "Italic" }
```

### mime_essence

Type: mapping of mime-type and mapping of mime-subtype and [NodeType Config][7]

Properties related to files with specific mime types are defined here.

It is possible to use the wildcard `*` to match all mime subtypes. It will be
overwritten by the more specific sub types that are defined.

Example:

```lua
xplr.config.node_types.mime_essence = {
  application = {
    -- application/*
    ["*"] = { meta = { icon = "a" } }

    -- application/pdf
    pdf = { meta = { icon = "" } },

    -- application/zip
    zip = { meta = { icon = ""} },
  },
}
```

### extension

Type: mapping of extension and [NodeType Config][7]

Properties related to files with specific extension are defined here.

Example:

```lua
xplr.config.node_types.extension.md = { meta = { icon = "" } }
xplr.config.node_types.extension.rs = { meta = { icon = "🦀" } }
```

### special

Type: mapping of name and [NodeType Config][7]

Properties related to files and directories with special names are defined
here.

Example:

```lua
xplr.config.node_types.special["Cargo.toml"] = { meta = { icon = "" } }
xplr.config.node_types.special["Downloads"] = { meta = { icon = "" } }
```

## NodeType Config

A node-type config contains the following fields:

- [meta][8]
- [style][9]

### meta

Type: mapping of string and string

A meta field can contain custom metadata about a node. By default, the "icon"
metadata is set for the [directory][1], [file][2], and
[symlink][3] nodes.

Example:

```lua
xplr.config.node_types.file = {
  meta = {
    icon = "f",
    foo = "bar",
  }
}
```

[1]: #directory
[2]: #file
[3]: #symlink
[4]: #mime_essence
[5]: #extension
[6]: #special
[7]: #nodetype-config
[8]: #meta
[9]: style.md
