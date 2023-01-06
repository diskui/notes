
the data model of git:

here is an example of git file structure:

```
root
|    \    
|     -> tree(folder)
|    /
|--foo
    --bar.txt -> blob(file)
|-bar.txt    /
```
this is a **recursive** structure, which means trees can contain trees.

the model of history:
```
                      add feature
O <------- O <----------O <-----------O
|                           / merge
|                          /
state                    /
                        O
                        fix bugs
```

the lower representation of tree and blob:
```
type blob = array<bytes>

type tree = map<string, tree | blob>

type commit = struct {
    parents:array<commit>
    author:string 
    message:string
    snapshot:tree
}

type object = blob | tree | commit

objects = map<string,object>

def store(o):
   id = sha1(o)
   objects[id] = o

def load(id):
   return objects[id]

reference = map<string,strint> // map human-readable message to hex code
```

some commands:

git log: visualize the commit history, to use it better, one can add some arguments, git log --all --graph --decorate

git diff: show what has changed since the last snapshot(head)

git diff hex-code file : shwo the changes of file since the hex-code commit

some rules to write git commit messages:
* Separate subject from body with a blank line
* Limit the subject line to 50 characters
* Capitalize the subject line
* Do not end the subject line with a period 
* Use the imperative mood in the subject line
* Wrap the body at 72 characters
* Use the body to explain what and why vs how









