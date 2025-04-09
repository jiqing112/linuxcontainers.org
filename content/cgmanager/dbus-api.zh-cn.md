# 当前API
当前API包含以下方法：

### Ping (int junk) -> None
Ping仅用于测试管理器是否存活，整数值将被忽略。

### GetPidCgroup (string controller, int pid) -> string cgroup
接收控制器名称和PID，返回对应的cgroup路径。

### GetPidCgroupAbs (string controller, int pid) -> string cgroup
接收控制器名称和PID，返回绝对cgroup路径。

### Create (string controller, string cgroup) -> int existed
在指定控制器中创建新cgroup路径，若路径已存在返回1，新创建返回0。

### Chown (string controller, string cgroup, int uid, int gid) -> None
修改指定控制器/cgroup路径的所有权为指定uid/gid，将同时修改目录及cgroup.procs/tasks文件。

### Chmod (string controller, string cgroup, string file, int mode) -> None
修改指定控制器/cgroup/文件的权限模式。

### MovePid (string controller, string cgroup, int pid) -> None
将指定PID移动到目标控制器/cgroup中。

### MovePidAbs (string controller, string cgroup, int pid) -> None
类似MovePid但使用绝对路径（而非相对于调用者的路径），此调用仅限root用户。

### GetValue (string controller, string cgroup, string key) -> string value
查询指定控制器/cgroup中键的值，返回值始终为字符串格式。

### SetValue (string controller, string cgroup, string key, string value) -> None
设置指定控制器/cgroup中键的值。

### Remove (string controller, string cgroup, int recursive) -> int existed
删除指定cgroup，recursive=1时递归删除子cgroup，返回值表示cgroup是否存在。

### GetTasks (string controller, string cgroup) -> array of int
返回包含指定cgroup中所有PID的整型数组。

### GetTasksRecursive (string controller, string cgroup) -> array of int
返回包含指定cgroup及其子目录中所有PID的整型数组。

### ListChildren (string controller, string cgroup) -> array of string
返回包含指定cgroup所有子cgroup的字符串数组。

### RemoveOnEmpty (string controller, string cgroup) -> None
标记cgroup为空时自动删除。当最后一个任务退出时，cgmanager将自动移除该cgroup。

### Prune (string controller, string cgroup) -> None
对cgroup路径及其