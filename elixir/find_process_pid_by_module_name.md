# Find Processes PID By Module Name

If you need to stop a running process that you don't know the PID, it's possible to filter all running processes by module name (or a part of it), retrieve the respective PIDs and then perform any needed action. The below snippet does exactly that by looking to the registered name property and filter any processes that might contain a certain string in its name. 

```elixir
processes_pids = 
  Process.list 
  |> Enum.filter(fn pid -> 
    Process.info(pid) 
    |> Keyword.get(:registered_name) 
    |> Atom.to_string() 
    |> String.contains?("BackgroundJob") 
  end)

# now we can perform actions such as terminate
Enum.each(processes_pids, fn pid -> Process.stop(pid, :shutdown) end) 

```
