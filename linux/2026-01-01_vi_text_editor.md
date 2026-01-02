<h1>Linux Command Line (VI Text Editor) </h1>

<h3>Starting VI </h3>

* `To Start` just type vi

  ```console
  Press ESC :q # to quit from vi if there are no changes made
  Press ESC :q! # to exit without saving even though you made changes
  Press ESC :w # to save current file
  Press ESC :w <file_name> # to save file as file_name
  Press ESC :wq # to write and quit
  ```

<h3>Different vi modes</h3>

* `Normal Mode` # to move around the file using arrow keys and other keys

   ```console
   # Start in normal mode by default
   Press w # move foward one word
   Press b # move backwards one word
   Press 0 # to get to the beginning of a line
   Press $ # to get to the end of a line 
   Press ctrl +f # to move foward one page at a time
   Press ctrl +b # to move back one page at a time
   Press shift g or Capital G # to go to the last line of a file
   Press <number>G # to go to any other line. 4+ shift g to go to the 4th line on the file
   Press o to open a new file
   Press ESC # when in other modes to return back to normal mode
   ```

* `Command Mode`  # where you can enter commands that performs tasks like writing or quitting 
   
   ```console
   Press : # To go from normal to command mode
   # status bar will be : to notify command mode
   :set # will show you all the vi variables currently in use. Press Enter to exit
   :set ruler # to tun on ruler
   :set norulter # to turn off ruler
   :set nu # add a line number to the left of the gile
   :set nonu # to turn off the numbers
   :set ic # ic means ignore case for example searching for bash /bash it will search for all teext that contains bash ignoring case
   :set noic # going back to case sensitive
   :r # will read the specifiged file or the output of a shell command
   :r !date # will run the system command for date and will print out the system date and time
   :r !lsblk -s # will display all the block device connected to the system such as hard dirves, thumb drives and more
   ```












