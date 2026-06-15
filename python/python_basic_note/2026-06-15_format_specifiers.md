<h1>Format Specifiers</h1>
Format specifiers when used in the context of a f string, they allow us to format a value based on what flags are inserted. Depending on what flags you insert, it will format your output a certain way. 

Following your value, you would type a colon : and a flag. {value:flags}. 

YOU CAN ALSO MIX FLAGS 
<h3>Flags</h3>
 ```console
 $ # :.(number)f = round to that many decimal place (fixed point). F = floating point number
 print(f"{3.14159:.2f}")
 $ # output:3.14

 $ #:(number) = allocate that many spaces. Added that many spaces before printing the output
 print(f"{3.14159:8}")
 $ # output:   3.14159
 
 $ # :< = left justify. Add to the total width of characters to the left. Pretty much just moves the characters to the left side of the screen. Think of making text in google docs and making all the characters move to the left side.
 text = "apple"
 print(f"there are {text:<12} left on the table")
 $ # output: there are apple       left on the table

 print(f"there are {text:!<7} left on the table")
 $ # output: there are apple!! left on the table
 
 $ # :> = right justify. Add to the total width of characters to the right. Think of googole docs and making all text move the right side of the screen.
 text = "apple"
 print(f"there are {text:>7} left on the table")
 $ # output: there are !!apple left on the table

 $ # :^ = center align. It makes the texts be align in the middle. Think of google docs and centering all text in the middle of the page
 text = "apple"
 print(f"there are {text:^7} left on the table")
 $ # output: there are !apple! left on the table

 $ # :+ = use a plus sign to indicate positive value. Same with negative value, just use minus sign
 num = 10
 print(f"there are {num:+} apples left on the table")
 $ # output: there are +10 apples left on the table

 $ # :, = uses to add comma on each thousand's place
 price = 17000
 print(f"the car cost ${price:,}")
 the car cost $17,000

 $ # mixing flags
 price = 17000.24234
 print(f"the car cost ${price:+,.2f}")
 $ # output: the car cost +17,000.24
 ```

