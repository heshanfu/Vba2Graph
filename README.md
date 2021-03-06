# Vba2Graph
A tool for security researchers, who waste their time analyzing malicious Office macros.

Generates a VBA call graph, with potential malicious keywords highlighted.

Allows for quick analysis of malicous macros, and easy understanding of the execution flow.

[@MalwareCantFly](https://twitter.com/MalwareCantFly)

### Features
- Keyword highlighting
- VBA Properties support
- External function declarion support
- Tricky macros with "\_Change" execution triggers
- Fancy color schemes!

#### Pros
&nbsp;&nbsp;&nbsp;&nbsp;✓ Pretty fast

&nbsp;&nbsp;&nbsp;&nbsp;✓ Works well on most malicious macros observed in the wild


#### Cons
&nbsp;&nbsp;&nbsp;&nbsp;✗ Static (dynamicaly resolved calls would not be recognized)



## Examples
Example 1:

Trickbot downloader - utilizes object Resize event as initial trigger, followed by TextBox_Change triggers.

![Example 1](https://github.com/MalwareCantFly/Vba2Graph/blob/master/Examples/5e9f29b946ea52344107e64fc89e603469bfe34278f295951be9b5b041058dba.png?raw=true)

Example 2:

![Example2](https://github.com/MalwareCantFly/Vba2Graph/blob/master/Examples/29c4d57ca968ec10ceb682ecf38a8e9bf89267eb5c88a33f71892164636cd190.png?raw=true)

Check out the *Examples* folder for more cases.
## Installation

### Install oletools:
```bash
https://github.com/decalage2/oletools/wiki/Install
```
### Install Python Requirements

```bash
pip2 install -r requirements.txt
```

### Install Graphviz

#### Windows 
Install Graphviz msi:
```bash
https://graphviz.gitlab.io/_pages/Download/Download_windows.html
```
Add "dot.exe" to PATH env variable or just:

```batch
set PATH=%PATH%;C:\Program Files (x86)\Graphviz2.38\bin
```

#### Mac
```bash
brew install graphviz
```

#### Ubuntu
```bash
sudo apt-get install graphviz
```

#### Arch
```bash
sudo pacman -S graphviz
```

### Usage

```bash
usage: vba2graph.py [-h] [-o OUTPUT] [-c {0,1,2,3}] (-i INPUT | -f FILE)

optional arguments:
  -h, --help            show this help message and exit
  -o OUTPUT, --output OUTPUT
                        output folder (default: "output")
  -c {0,1,2,3}, --colors {0,1,2,3}
                        color scheme number [0, 1, 2, 3] (default: 0 - B&W)
  -i INPUT, --input INPUT
                        olevba generated file or .bas file
  -f FILE, --file FILE  Office file with macros

```
### Usage Examples (All Platforms)
Only Python 2 is supported:
```bash
# Generate call graph directly from an Office file with macros [tnx @doomedraven]
python2 vba2graph.py -f malicious.doc -c 2    

# Generate vba code using olevba then pipe it to vba2graph
olevba malicious.doc | python2 vba2graph.py -c 1

# Generate call graph from VBA code
python2 vba2graph.py -i vba_code.bas -o output_folder

```

### Output
You'll get 4 folders in your output folder:

- **png:** the actual graph image you are looking for
- **svg:** same graph image, just in vector graphics
- **dot:** the dot file which was used to create the graph image
- **bas:** the VBA functions code that was recognized by the script (for debugging)

### Batch Processing
#### Mac/Linux:

**batch.sh** script file is attached for running *olevba* and *vba2graph* on an input folder of malicious docs.

Deletes *output* dir. use with caution.
