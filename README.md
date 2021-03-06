#JCDP

**Java Colored Debug Printer** (JCDP) is a Java library that offers you a convenient way to print colored messages or debug messages on a terminal.

###Download

You can download the .jar package at [JCDP's official webpage](http://diogonunes.com/it/work/jcdp/#download). I have uploaded both a Windows/Linux version and a Linux-only version (the latter is lighter and has no dependencies over external libs).

###How to use it

The following code should produce [this result](http://www.diogonunes.com/it/work/jcdp/#example).

```java
package print.test;
 
import print.Printer;
import print.Printer.Types;
import print.color.ColoredPrinter;
import print.color.Ansi.*;
import print.exception.InvalidArgumentsException;
 
public class ExampleApp {
    public static void main(String[] args) throws InvalidArgumentsException {
 
        //example of a terminal Printer
        Printer p = new Printer.Builder(Types.TERM).build();
        p.println(p);
        p.println("This is a normal message.");
        p.errorPrintln("This is an error message.");
        p.debugPrintln("This debug message is always printed.");
        p = new Printer.Builder(Types.TERM).level(1).timestamping(false).build();
        p.println(p);
        p.debugPrintln("This is printed because its level is <= 1", 1);
        p.debugPrintln("This isn't printed because its level is > 1", 2);
        p.setLevel(2);
        p.debugPrintln("Now this is printed because its level is <= 2", 2);
         
        //example of a Colored terminal Printer (WINDOWS or UNIX)
        ColoredPrinter cp = new ColoredPrinter.Builder(1, false)
                                .foreground(FColor.WHITE).background(BColor.BLUE)   //setting format
                                .build();
            //printing according to that format
        cp.println(cp);
        cp.setAttribute(Attribute.REVERSE);
        cp.println("This is a normal message (with format reversed).");
            //reseting the terminal to its default colors
        cp.clear();
        cp.print(cp.getDateTime(), Attribute.NONE, FColor.CYAN, BColor.BLACK);
        cp.debugPrintln(" This debug message is always printed.");
        cp.clear();
        cp.print("This example used JCDP 1.25   ");
            //temporarily overriding that format
        cp.print("\tMADE ", Attribute.BOLD, FColor.YELLOW, BColor.GREEN);
        cp.print("IN PORTUGAL\t\n", Attribute.BOLD, FColor.YELLOW, BColor.RED);
        cp.println("I hope you find it useful ;)");
 
        cp.clear(); //don't forget to clear the terminal's format before exiting                      
    }
}
```

###Documentation

For more information about how to use this library please check [JCDP's official webpage](http://diogonunes.com/it/work/jcdp/). If you want to read the *javadoc* you can check the `doc` folder or read it [online](http://diogonunes.com/it/work/jcdp/doc/index.html).

###Future Work

- Create a FilePrinter, an implementation that prints to a file rather than a terminal.