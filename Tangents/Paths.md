# What the hell are paths?
So, you guys have folders and files on your devices, right?  There's this thing called a filesystem that allows the folders/files to keep their structure of one inside the other x has n different pdf's in it or whatever, you get the idea. The filesystem is what enables you to have a sort of organized way of storing your files.

Now, path is a way to specify the location of a file or folder within a file system. It's just like an address that represents the sequence of directories (cities) and subdirectories (streets) that lead to a particular file or folder (destination).

Think of it like a map that shows how to get to a specific location. Just as a map might say "start at the city center, go north on Main St, turn left on Elm St, and arrive at 123 Elm St", a path in a file system might say "start at the root directory, go into the 'Documents' folder, then into the 'PDFs' folder, and arrive at the file 'example.pdf'".

Paths can be absolute or relative. An absolute path starts from the root directory and specifies the entire sequence of directories and subdirectories to reach a file or folder. A relative path, on the other hand, starts from the current working directory and specifies the sequence of directories and subdirectories to reach a file or folder relative to the current location.

For example, an absolute path might be `/home/username/Documents/PDFs/example.pdf`, while a relative path might be `./PDFs/example.pdf` (assuming the current working directory is `Documents`).

## Relative paths
Typing out the entire path to access a given thing can be tedious if you have to do it repeatedly. therefore people came up with relative paths, you can think of this as more like someone on the phone telling you how to get somewhere, they don't give you the full address, they ask you where you are, and then tell you how to get to the destination from where you are.

**CWD**: CWD stands for Current Working Directory, it is the directory that is currently active, and can be thought of like your current location

relative paths heavily use `.` - which denotes the current directory and `..` - which denotes the parent directory. For example if you are in `/home/username/Desktop`, then `..` would denote the directory `/home/username` which is it's parent, in other words, it goes 1 level upwards.

I highly encourage you play around with this in your terminal to get a feel for how paths work.

Here are some examples
assuming your CWD is `/home/username/Desktop`, you can use the following relative paths:
- `.` to refer to the current directory (`/home/username/Desktop`)
- `..` to refer to the parent directory (`/home/username`)
- `./Documents` to refer to a subdirectory called `Documents` within the current directory (`/home/username/Desktop/Documents`)
- `../Documents` to refer to a subdirectory called `Documents` within the parent directory (`/home/username/Documents`)


This is just a simple overview on paths, there are a huge amount of commands which operate on your CWD and take in paths (both relative and absolute as arguments)