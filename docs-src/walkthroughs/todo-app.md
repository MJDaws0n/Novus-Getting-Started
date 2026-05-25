# Building the Todo app

The [Todo-App](https://github.com/MJDaws0n/Todo-App) is a good CLI example because it stays simple:

- parse arguments
- load a file
- update data
- write the file back

## Imports

```novus
import lib/std;
import lib/file_io;
```

This is an older import style, but it still shows an important point: small Novus applications can be built from only a couple of libraries.

## Command parsing

The app starts by checking the subcommand:

```novus
let supportedOperation: []str =['help', 'list' ,'add', 'check'];
let operation: str = str_lower(argv_get(argv, 1));

if(!array_contains_str(supportedOperation, operation)){
    print('Incorrect Usage');
    printUsage();
    exit(2);
}
```

That is a classic Novus CLI pattern:

- read `argv`
- normalise input
- validate against an allowed list

## Reading tasks

Tasks live in a plain text file and are parsed into an array:

```novus
fn getTasks() -> []str {
    let tasksFile: str = getTasksFileLocation();
    if(!file_exists(tasksFile)){
        return [];
    }

    let tasksStr: str = read_file(tasksFile);
    let tasks: []str = [];

    while (tasksStr != '') {
        let task: str = str_split_first(tasksStr, "\n");
        if (task != '') {
            array_append(tasks, task);
        }

        tasksStr = str_split_rest(tasksStr, "\n");
    }

    return tasks;
}
```

The design is intentionally simple and easy to debug.

## Writing tasks

Adding a task just appends a new line in the app's custom pipe-delimited format:

```novus
fn addTask(newTask: str) -> i32{
    let tasksFile: str = getTasksFileLocation();
    let currentTasks: str = '';

    if(file_exists(tasksFile)){
        currentTasks = read_file(tasksFile) + '\n';
    }

    let taskid: i32 = array_len_str(getTasks()) + 1;
    currentTasks = currentTasks + i32_to_str(taskid) + '|' + newTask + '|0';

    if (write_file(tasksFile, currentTasks) != 0) {
        print('An error occured saving the task');
        exit(1);
    }

    return taskid;
}
```

## Toggling completion

The app rewrites the whole file after flipping the task state:

```novus
fn checkTask(taskid: i32) -> []str {
    ...
    updatedTasks = updatedTasks + "\n" + taskParts[0] + '|' + taskParts[1] + '|' + taskParts[2];
    ...
    if (write_file(tasksFile, updatedTasks) != 0) {
        print('An error occured saving the task');
        exit(1);
    }
    ...
}
```

That is not the most sophisticated storage model, but it is a very good learning example because every step is visible.

## Why this example matters

The Todo app shows how to:

- build a CLI entrypoint
- validate arguments
- read and write plain files
- use arrays of strings as application state
- keep an application entirely in Novus

If the platformer shows the graphical side of the ecosystem, the Todo app shows the command-line side.

