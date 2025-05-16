# llm-agent

A program that queries Claude and can run tools. I took this from a tutorial: https://ampcode.com/how-to-build-an-agent

```
    $ go run .
    Chat with Claude (use 'ctrl-c' to quit)
    You: Hey Claude, please read main.go and propose a few options for new tools that would be easy to implement and generally useful.
    Claude: I'll read the main.go file to see what's currently implemented and propose some new tools that would be useful additions.
    tool: read_file({"path":"main.go"})
    Claude: After examining main.go, I can propose several new tools that would be easy to implement and generally useful:

    ### 1. `create_file` Tool
    This would allow creating a new file with content more directly than using edit_file with an empty old_str.

    ```go
    type CreateFileInput struct {
        Path    string `json:"path" jsonschema_description:"The path where the file should be created"`
        Content string `json:"content" jsonschema_description:"The content to write to the file"`
        Mode    int    `json:"mode,omitempty" jsonschema_description:"Optional file permissions (defaults to 0644)"`
    }
    ```

    ### 2. `delete_file` Tool
    This would allow removing files from the filesystem.

    ```go
    type DeleteFileInput struct {
        Path string `json:"path" jsonschema_description:"The path of the file to delete"`
    }
    ```

    ### 3. `execute_command` Tool
    This would enable running shell commands and capturing their output.

    ```go
    type ExecuteCommandInput struct {
        Command     string   `json:"command" jsonschema_description:"The command to execute"`
        Args        []string `json:"args,omitempty" jsonschema_description:"Optional command arguments"`
        WorkingDir  string   `json:"working_dir,omitempty" jsonschema_description:"Optional working directory (defaults to current directory)"`
        Environment []string `json:"environment,omitempty" jsonschema_description:"Optional environment variables in KEY=VALUE format"`
    }
    ```

    ### 4. `search_files` Tool
    This would search for files containing specific text or matching patterns.

    ```go
    type SearchFilesInput struct {
        Query       string `json:"query" jsonschema_description:"Text to search for in files"`
        Path        string `json:"path,omitempty" jsonschema_description:"Path to search in (defaults to current directory)"`
        Recursive   bool   `json:"recursive,omitempty" jsonschema_description:"Whether to search recursively (defaults to true)"`
        IgnoreCase  bool   `json:"ignore_case,omitempty" jsonschema_description:"Whether to ignore case when searching (defaults to false)"`
        MaxResults  int    `json:"max_results,omitempty" jsonschema_description:"Maximum number of results to return (defaults to 100)"`
        FilePattern string `json:"file_pattern,omitempty" jsonschema_description:"Optional pattern to filter files (e.g., '*.go')"`
    }
    ```

    ### 5. `rename_file` Tool
    This would make it easy to rename files or move them to different locations.

    ```go
    type RenameFileInput struct {
        OldPath string `json:"old_path" jsonschema_description:"The current path of the file"`
        NewPath string `json:"new_path" jsonschema_description:"The new path for the file"`
    }
    ```

    ### 6. `read_directory_tree` Tool
    This would provide a more structured directory tree representation than list_files.

    ```go
    type ReadDirectoryTreeInput struct {
        Path      string `json:"path,omitempty" jsonschema_description:"Root path to start from (defaults to current directory)"`
        MaxDepth  int    `json:"max_depth,omitempty" jsonschema_description:"Maximum depth to traverse (defaults to 3)"`
        ShowFiles bool   `json:"show_files,omitempty" jsonschema_description:"Whether to include files in output (defaults to true)"`
    }
    ```

    Each of these tools would extend the capabilities of the current system while following the existing pattern of implementation. They would significantly enhance the system's ability to interact with the filesystem and environment in useful ways.
```