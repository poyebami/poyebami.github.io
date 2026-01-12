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

* `Normal Mode` to move around the file using arrow keys and other keys

   ```console
   # Start in normal mode by default
   $ Press w # move foward one word
   $ Press b # move backwards one word
   $ Press 0 # to get to the beginning of a line
   $ Press $ # to get to the end of a line 
   $ Press ctrl +f # to move foward one page at a time
   $ Press ctrl +b # to move back one page at a time
   $ Press shift g or Capital G # to go to the last line of a file
   $ Press <number>G # to go to any other line. 4+ shift g to go to the 4th line on the file
   $ Press o to open a new file
   $ # move current line to the top of the screen
   $ zt
   $ # center line
   $ zz
   $ # move current line to bottom
   $ zb
   $ Press ESC # when in other modes to return back to normal mode
   ```

* `Command Mode` where you can enter commands that performs tasks like writing or quitting 
   
   ```console
   $ Press : # To go from normal to command mode
    # status bar will be : to notify command mode
   $ :set # will show you all the vi variables currently in use. Press Enter to exit
   $ :set ruler # to tun on ruler
   $ :set norulter # to turn off ruler
   $ :set nu # add a line number to the left of the gile
   $ :set nonu # to turn off the numbers
   $ :set ic # ic means ignore case for example searching for bash /bash it will search for all teext that contains bash ignoring case
   $ :set noic # going back to case sensitive
   $ :r # will read the specifiged file or the output of a shell command
   $ :r !date # will run the system command for date and will print out the system date and time
   $ :r !lsblk -s # will display all the block device connected to the system such as hard dirves, thumb drives and more
   ```

* `Insert Mode` where you are inserting characters /text into a documents

  ```console
   $ Press i # enter to insert mode
   $ # You will see -- INSERT -- at the status bar to let you that you are in insert mode
   $ Press a # append text after the cursor
   $ Press o # open a new line below the cursor
   $ Press r # replace one character at the cursor. <Text> will be <Test>
   $ Press x # to delete a character that the cursor is on
   $ <Number>x # delete the number of characters starting from where the character is. <5x> will deelte 5 character starting from the cursor prepend the x with a number of characters to delete
   $ dw # delete a word from teh cursor
   $ dd # delete the line where the cursor is
   $ <Number>dd # delete the number of lines at the cursor. <4dd> will delete 4 lines at teh cursor prepend the dd command with the number of lines to delete.
  ```
  ```console
   $ :%s/find_this_repalce_with/g
   Line range specifier
   $ % # means to do the operation on all lines
   $ 1,6 # means to do the operations on lines 1-6
   $ S # stands for search
   $ /find_this # for text search
   $ /repalce_with # for text to substitute with
   $ / # end the set
   $ g # optional but its means global substitution and means to do this for every occurrence on a line. Otherwise the substitute will only occur for the first occurrence.
   $ # the status bar will tell you the <number> of substitutions on <number> of line

   For specific lines
   $ :4,9s/find_this/replace_with/g

   $ Press u # undo; roll back changes while in normal mode
   $ # For line ranges there are special characters
   $ # . for current line indicator
   $ # $ for the last line indicator

   $ To replace object found with <nothing> //
   $ :.,$s/HOME// #will place HOME with nothing starting from the current line to the last line
  ```

* `Replace Mode` where the text you are typing replace the existing text in the document

  ```console
   $ Press Capital R # enter in replace mode

   YANKING AND PUTTING
   $ Press y # to yank the line into the paste buffer. This will copy entire line
   $ Press P # paste contents of paste buffer above the cursor
   $ Press p $ paste contents of paste buffer below the cursor

   SEARCH AND SUBSTITUTE
   $ /<name_of_text> # to get into search mode and hitting enter, it will move cursor to where it found the text
   $ Press n # to find the next occurrence of the search term
   $ # receive a warning saying "search hit BOTTOM, continuing at TOP"
   $ ?<name_of_text> # to search backwards
   $ # press n but going backwards and teh same warning but "TOP, continuing at BOTTOM 
  ```
  









