//Zach Eddington
/*Write a program in C# using a console application that demonstrates 
the use of a Stack, Queue, and Dictionary (Map). I want you to start 
trying to use GitHub for this assignment.

 Your application will be based around a simple menu. The functionality
 of each menu item is described in more detail below. The first menu
 prompt should be the following:
 
1. Stack
2. Queue
3. Dictionary
4. Exit

If the user chooses #1, display:

1. Add one time to Stack
2. Add Huge List of Items to Stack
3. Display Stack
4. Delete from Stack
5. Clear Stack
6. Search Stack
7. Return to Main Menu

If the user chooses #2, display:

1. Add one time to Queue
2. Add Huge List of Items to Queue
3. Display Queue
4. Delete from Queue
5. Clear Queue
6. Search Queue
7. Return to Main Menu

If the user chooses #3, display:

1. Add one item to Dictionary
2. Add Huge List of Items to Dictionary
3. Display Dictionary
4. Delete from Dictionary
5. Clear Dictionary
6. Search Dictionary
7. Return to Main Menu */

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Diagnostics;

namespace ConsoleApp1
{
    class Program
    {
        static void Main(string[] args)
        {
            //Create Stack, Queue, Dictionary, and Stopwatch objects for project
            Stack<string> stStackMain = new Stack<string>();
            Stack<string> stStackSave = new Stack<string>();
            Queue<string> qQueueMain = new Queue<string>();
            Queue<string> qQueueSave = new Queue<string>();
            Dictionary<string, int> dDictionaryMain = new Dictionary<string, int>();
            Stopwatch swStopWatch = new Stopwatch();

            //Declare all variables used in project
            string sMainSelection;
            string sStackSelection;
            string sQueueSelection;
            string sDictionarySelection;
            string sDeleteSelection;
            string sUserInput;
            bool bValid;
            bool bFound;
            int iCount;
            int iNumDeleted;
            int iDictionaryCount;

            do
            {
                //Prints the main menu in console and asks for user input to select a choice
                Console.WriteLine("\n1. Stack");
                Console.WriteLine("2. Queue");
                Console.WriteLine("3. Dictionary");
                Console.WriteLine("4. Exit");
                sMainSelection = Console.ReadLine();
                Console.WriteLine("--------------------");
                do
                {
                    //Switch case statement that is determined by main menu user input
                    switch (sMainSelection)
                    {
                        //Stack
                        case "1":
                            Console.WriteLine("\n1. Add one time to Stack");
                            Console.WriteLine("2. Add Huge List of Items to Stack");
                            Console.WriteLine("3. Display Stack");
                            Console.WriteLine("4. Delete from Stack");
                            Console.WriteLine("5. Clear Stack");
                            Console.WriteLine("6. Search Stack");
                            Console.WriteLine("7. Return to Main Menu");
                            sStackSelection = Console.ReadLine();
                            Console.WriteLine("--------------------\n");
                            do
                            {
                                switch (sStackSelection)
                                {
                                    //Add one time to Stack
                                    case "1":
                                        Console.WriteLine("\nEnter a string to add to the stack");
                                        stStackMain.Push(Console.ReadLine());
                                        Console.WriteLine("\n" + stStackMain.Count + " item(s) in stack\n");
                                        bValid = true;
                                        break;
                                    //Add Huge List of Items to Stack
                                    case "2":
                                        stStackMain.Clear();
                                        for (iCount = 1; iCount <= 2000; iCount++)
                                        {
                                            stStackMain.Push("New Entry " + iCount);
                                        }
                                        Console.WriteLine("\n" + stStackMain.Count + " item(s) in stack");
                                        bValid = true;
                                        break;
                                    //Display Stack
                                    case "3":
                                        if (stStackMain.Count != 0)
                                        {
                                            //Pops main stack into save stack so it can be printed off in numerical order
                                            while (stStackMain.Count > 0)
                                            {
                                                stStackSave.Push(stStackMain.Pop());
                                            }
                                            //Printed in numerical order through save stack
                                            foreach (string value in stStackSave)
                                            {
                                                Console.WriteLine(value);
                                            }
                                            //Put back into main stack from save stack
                                            while (stStackSave.Count > 0)
                                            {
                                                stStackMain.Push(stStackSave.Pop());
                                            }
                                        }
                                        else
                                        {
                                            Console.WriteLine("\nThere are no items in the stack");
                                        }
                                        bValid = true;
                                        break;
                                    //Delete from Stack
                                    case "4":
                                        iNumDeleted = 0;
                                        Console.WriteLine("What value would you like to delete from the stack?");
                                        sDeleteSelection = Console.ReadLine();
                                        while (stStackMain.Count > 0)
                                        {
                                            //Checks if next value is the value they want to delete
                                            //If so, it is popped off and the deleted counter is incrimented
                                            if (stStackMain.Peek() == sDeleteSelection)
                                            {
                                                stStackMain.Pop();
                                                iNumDeleted++;
                                            }
                                            //If not, it is popped onto the save stack
                                            else
                                            {
                                                stStackSave.Push(stStackMain.Pop());
                                            }
                                        }
                                        //Once the whole stack has been gone through, the save stack is put back on main stack
                                        for (iCount = 0; stStackSave.Count > 0; iCount++)
                                        {
                                            stStackMain.Push(stStackSave.Pop());
                                        }
                                        //Number of deleted values is printed in console
                                        if (iNumDeleted != 0)
                                        {
                                            Console.WriteLine("\n" + iNumDeleted + " value(s) deleted");
                                        }
                                        //If the searched value is not found in the stack, a notice is given to the user
                                        else
                                        {
                                            Console.WriteLine("\nThere were no values in the stack that matched your entry");
                                            Console.WriteLine("If you want to delete something, please enter a value contained in the stack");
                                        }
                                        bValid = true;
                                        break;
                                    //Clear Stack
                                    case "5":
                                        Console.WriteLine(stStackMain.Count + " item(s) cleared from stack\n");
                                        stStackMain.Clear();
                                        bValid = true;
                                        break;
                                    //Search Stack
                                    case "6":
                                        Console.WriteLine("What value do you want to search for in the stack?");
                                        sUserInput = Console.ReadLine();
                                        swStopWatch.Start();
                                        bFound = stStackMain.Contains(sUserInput);
                                        swStopWatch.Stop();
                                        //Informs user if the value was found or not and shows the elapsed time
                                        if (bFound)
                                        {
                                            Console.WriteLine("\nThe value \"" + sUserInput + "\" WAS found. It took " + swStopWatch.Elapsed);
                                        }
                                        else
                                        {
                                            Console.WriteLine("\nThe value \"" + sUserInput + "\" WAS NOT found. It took " + swStopWatch.Elapsed);
                                        }
                                        bValid = true;
                                        break;
                                    //Return to Main Menu
                                    case "7":
                                        bValid = true;
                                        break;
                                    //Invalid Input
                                    default:
                                        Console.WriteLine("\nPlease enter a valid input");
                                        sStackSelection = Console.ReadLine();
                                        bValid = false;
                                        break;
                                }
                            } while (bValid == false);
                            if (sStackSelection == "7")
                            {
                                bValid = true;
                            }
                            else
                            {
                                bValid = false;
                            }
                            break;

                        //Queue
                        case "2":
                            Console.WriteLine("\n1. Add one time to Queue");
                            Console.WriteLine("2. Add Huge List of Items to Queue");
                            Console.WriteLine("3. Display Queue");
                            Console.WriteLine("4. Delete from Queue");
                            Console.WriteLine("5. Clear Queue");
                            Console.WriteLine("6. Search Queue");
                            Console.WriteLine("7. Return to Main Menu");
                            sQueueSelection = Console.ReadLine();
                            Console.WriteLine("--------------------\n");
                            do
                            {
                                switch (sQueueSelection)
                                {
                                    //Add one time to Queue
                                    case "1":
                                        Console.WriteLine("\nEnter a string to add to the queue");
                                        qQueueMain.Enqueue(Console.ReadLine());
                                        Console.WriteLine("\n" + qQueueMain.Count + " item(s) in queue\n");
                                        bValid = true;
                                        break;
                                    //Add Huge List of Items to Queue
                                    case "2":
                                        qQueueMain.Clear();
                                        for (iCount = 1; iCount <= 2000; iCount++)
                                        {
                                            qQueueMain.Enqueue("New Entry " + iCount);
                                        }
                                        Console.WriteLine("\n" + qQueueMain.Count + " item(s) in queue");
                                        bValid = true;
                                        break;
                                    //Display Queue
                                    case "3":
                                        if (qQueueMain.Count != 0)
                                        {
                                            foreach (string value in qQueueMain)
                                            {
                                                Console.WriteLine(value);
                                            }
                                        }
                                        else
                                        {
                                            Console.WriteLine("\nThere are no items in the queue");
                                        }
                                        bValid = true;
                                        break;
                                    //Delete from Queue
                                    case "4":
                                        iNumDeleted = 0;
                                        Console.WriteLine("What value would you like to delete?");
                                        sDeleteSelection = Console.ReadLine();
                                        //Checks if next value is the value they want to delete
                                        //If so, it is dequeued and the deleted counter is incrimented
                                        while (qQueueMain.Count > 0)
                                        {
                                            if (qQueueMain.Peek() == sDeleteSelection)
                                            {
                                                qQueueMain.Dequeue();
                                                iNumDeleted++;
                                            }
                                            //If not, it is queued onto the save queue
                                            else
                                            {
                                                qQueueSave.Enqueue(qQueueMain.Dequeue());
                                            }
                                        }
                                        //Once the whole stack has been gone through, the save stack is put back on main stack
                                        for (iCount = 0; qQueueSave.Count > 0; iCount++)
                                        {
                                            qQueueMain.Enqueue(qQueueSave.Dequeue());
                                        }
                                        //Number of deleted values are printed in console
                                        if (iNumDeleted != 0)
                                        {
                                            Console.WriteLine("\n" + iNumDeleted + " value(s) deleted");
                                        }
                                        //If the searched value is not found in the stack, a notice is given to the user
                                        else
                                        {
                                            Console.WriteLine("\nThere were no values that matched your entry");
                                            Console.WriteLine("If you want to delete something, please enter a value contained in the queue");
                                        }
                                        bValid = true;
                                        break;
                                    //Clear Queue
                                    case "5":
                                        Console.WriteLine(qQueueMain.Count + " item(s) cleared from queue\n");
                                        stStackMain.Clear();
                                        bValid = true;
                                        break;
                                    //Search Queue
                                    case "6":
                                        Console.WriteLine("What value do you want to search for in the queue?");
                                        sUserInput = Console.ReadLine();
                                        swStopWatch.Start();
                                        bFound = qQueueMain.Contains(sUserInput);
                                        swStopWatch.Stop();
                                        //Informs user if the value was found or not and shows the elapsed time
                                        if (bFound)
                                        {
                                            Console.WriteLine("\nThe value \"" + sUserInput + "\" WAS found. It took " + swStopWatch.Elapsed);
                                        }
                                        else
                                        {
                                            Console.WriteLine("\nThe value \"" + sUserInput + "\" WAS NOT found. It took " + swStopWatch.Elapsed);
                                        }
                                        bValid = true;
                                        break;
                                    //Return to Main Menu
                                    case "7":
                                        bValid = true;
                                        break;
                                    //Invalid Input
                                    default:
                                        Console.WriteLine("\nPlease enter a valid input");
                                        sQueueSelection = Console.ReadLine();
                                        bValid = false;
                                        break;
                                }
                            } while (bValid == false);
                            if (sQueueSelection == "7")
                            {
                                bValid = true;
                            }
                            else
                            {
                                bValid = false;
                            }
                            break;

                        //Dictionary
                        case "3":
                            Console.WriteLine("\n1. Add one time to Dictionary");
                            Console.WriteLine("2. Add Huge List of Items to Dictionary");
                            Console.WriteLine("3. Display Dictionary");
                            Console.WriteLine("4. Delete from Dictionary");
                            Console.WriteLine("5. Clear Dictionary");
                            Console.WriteLine("6. Search Dictionary");
                            Console.WriteLine("7. Return to Main Menu");
                            sDictionarySelection = Console.ReadLine();
                            Console.WriteLine("--------------------\n");
                            do
                            {
                                switch (sDictionarySelection)
                                {
                                    //Add one time to Dictionary
                                    case "1":
                                        Console.WriteLine("\nEnter a string to add to the dictionary");
                                        dDictionaryMain.Add(Console.ReadLine() + " ", dDictionaryMain.Count + 1);
                                        Console.WriteLine("\n" + dDictionaryMain.Count + " item(s) in dictionary\n");
                                        bValid = true;
                                        break;
                                    //Add Huge List of Items to Dictionary
                                    case "2":
                                        dDictionaryMain.Clear();
                                        for (iCount = 1; iCount <= 2000; iCount++)
                                        {
                                            dDictionaryMain.Add("New Entry " + iCount, dDictionaryMain.Count + 1);
                                        }
                                        Console.WriteLine("\n" + dDictionaryMain.Count + " item(s) in dictionary");
                                        bValid = true;
                                        break;
                                    //Display Dictionary
                                    case "3":
                                        if (dDictionaryMain.Count != 0)
                                        {
                                            foreach (KeyValuePair<string, int> KeyValue in dDictionaryMain)
                                            {
                                                Console.WriteLine("{0}", KeyValue.Key);
                                            }
                                        }
                                        else
                                        {
                                            Console.WriteLine("\nThere are no items in the dictionary");
                                        }
                                        bValid = true;
                                        break;
                                    //Delete from Dictionary
                                    case "4":
                                        Console.WriteLine("What value would you like to delete?");
                                        iDictionaryCount = dDictionaryMain.Count;
                                        dDictionaryMain.Remove(Console.ReadLine());
                                        iNumDeleted = iDictionaryCount = dDictionaryMain.Count;
                                        //Takes original dictionary count and subtracts the new dictionary count
                                        //If the subtracted value is not 0, the value is given as number of values deleted
                                        if (iNumDeleted != 0)
                                        {
                                            Console.WriteLine("\n" + iNumDeleted + " value(s) deleted");
                                        }
                                        //If the subtracted value is 0, the user is notified
                                        else
                                        {
                                            Console.WriteLine("\nThere were no values that matched your entry");
                                            Console.WriteLine("If you want to delete something, please enter a value contained in the dictionary");
                                        }
                                        bValid = true;
                                        break;
                                    //Clear Dictionary
                                    case "5":
                                        Console.WriteLine(dDictionaryMain.Count + " item(s) cleared from dictionary\n");
                                        dDictionaryMain.Clear();
                                        bValid = true;
                                        break;
                                    //Search Dictionary
                                    case "6":
                                        Console.WriteLine("What value do you want to search for in the dictionary?");
                                        sUserInput = Console.ReadLine();
                                        swStopWatch.Start();
                                        bFound = dDictionaryMain.ContainsKey(sUserInput);
                                        swStopWatch.Stop();
                                        //Informs user if the value was found or not and shows the elapsed time
                                        if (bFound)
                                        {
                                            Console.WriteLine("\nThe value \"" + sUserInput + "\" WAS found. It took " + swStopWatch.Elapsed);
                                        }
                                        else
                                        {
                                            Console.WriteLine("\nThe value \"" + sUserInput + "\" WAS NOT found. It took " + swStopWatch.Elapsed);
                                        }
                                        bValid = true;
                                        break;
                                    //Return to Main Menu
                                    case "7":
                                        bValid = true;
                                        break;
                                    //Invalid Input
                                    default:
                                        Console.WriteLine("\nPlease enter a valid input");
                                        sQueueSelection = Console.ReadLine();
                                        bValid = false;
                                        break;
                                }
                            } while (bValid == false);
                            if (sDictionarySelection == "7")
                            {
                                bValid = true;
                            }
                            else
                            {
                                bValid = false;
                            }
                            break;
                        //Exit program
                        case "4":
                            bValid = true;
                            break;
                        //Invalid number on main menu
                        default:
                            Console.WriteLine("\nPlease enter a valid input");
                            sMainSelection = Console.ReadLine();
                            bValid = false;
                            break;
                    }
                } while (bValid == false);
            } while (sMainSelection != "4");
        }
    }
}
