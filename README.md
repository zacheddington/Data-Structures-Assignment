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
            Stack<string> stStackMain = new Stack<string>();
            Stack<string> stStackSave = new Stack<string>();
            Queue<string> qQueueMain = new Queue<string>();
            Queue<string> qQueueSave = new Queue<string>();
            Dictionary<string, int> dDictionaryMain = new Dictionary<string, int>();
            Stopwatch swStopWatch = new Stopwatch();
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
                Console.WriteLine("\n1. Stack");
                Console.WriteLine("2. Queue");
                Console.WriteLine("3. Dictionary");
                Console.WriteLine("4. Exit");
                sMainSelection = Console.ReadLine();
                Console.WriteLine("--------------------");
                do
                {
                    switch (sMainSelection)
                    {
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
                                    case "1":
                                        Console.WriteLine("\nEnter a string to add to the stack");
                                        stStackMain.Push(Console.ReadLine());
                                        Console.WriteLine("\n" + stStackMain.Count + " item(s) in stack\n");
                                        bValid = true;
                                        break;
                                    case "2":
                                        stStackMain.Clear();
                                        for (iCount = 1; iCount <= 2000; iCount++)
                                        {
                                            stStackMain.Push("New Entry " + iCount);
                                        }
                                        Console.WriteLine("\n" + stStackMain.Count + " item(s) in stack");
                                        bValid = true;
                                        break;
                                    case "3":
                                        if (stStackMain.Count != 0)
                                        {
                                            while (stStackMain.Count > 0)
                                            {
                                                stStackSave.Push(stStackMain.Pop());
                                            }
                                            foreach (string value in stStackSave)
                                            {
                                                Console.WriteLine(value);
                                            }
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
                                    case "4":
                                        iNumDeleted = 0;
                                        Console.WriteLine("What value would you like to delete from the stack?");
                                        sDeleteSelection = Console.ReadLine();
                                        while (stStackMain.Count > 0)
                                        {
                                            if (stStackMain.Peek() == sDeleteSelection)
                                            {
                                                stStackMain.Pop();
                                                iNumDeleted++;
                                            }
                                            else
                                            {
                                                stStackSave.Push(stStackMain.Pop());
                                            }
                                        }
                                        for (iCount = 0; stStackSave.Count > 0; iCount++)
                                        {
                                            stStackMain.Push(stStackSave.Pop());
                                        }
                                        if (iNumDeleted != 0)
                                        {
                                            Console.WriteLine("\n" + iNumDeleted + " value(s) deleted");
                                        }
                                        else
                                        {
                                            Console.WriteLine("\nThere were no values in the stack that matched your entry");
                                            Console.WriteLine("If you want to delete something, please enter a value contained in the stack");
                                        }
                                        bValid = true;
                                        break;
                                    case "5":
                                        Console.WriteLine(stStackMain.Count + " item(s) cleared from stack\n");
                                        stStackMain.Clear();
                                        bValid = true;
                                        break;
                                    case "6":
                                        Console.WriteLine("What value do you want to search for in the stack?");
                                        sUserInput = Console.ReadLine();
                                        swStopWatch.Start();
                                        bFound = stStackMain.Contains(sUserInput);
                                        swStopWatch.Stop();
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
                                    case "7":
                                        bValid = true;
                                        break;
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
                                    case "1":
                                        Console.WriteLine("\nEnter a string to add to the queue");
                                        qQueueMain.Enqueue(Console.ReadLine());
                                        Console.WriteLine("\n" + qQueueMain.Count + " item(s) in queue\n");
                                        bValid = true;
                                        break;
                                    case "2":
                                        qQueueMain.Clear();
                                        for (iCount = 1; iCount <= 2000; iCount++)
                                        {
                                            qQueueMain.Enqueue("New Entry " + iCount);
                                        }
                                        Console.WriteLine("\n" + qQueueMain.Count + " item(s) in queue");
                                        bValid = true;
                                        break;
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
                                    case "4":
                                        iNumDeleted = 0;
                                        Console.WriteLine("What value would you like to delete?");
                                        sDeleteSelection = Console.ReadLine();
                                        while (qQueueMain.Count > 0)
                                        {
                                            if (qQueueMain.Peek() == sDeleteSelection)
                                            {
                                                qQueueMain.Dequeue();
                                                iNumDeleted++;
                                            }
                                            else
                                            {
                                                qQueueSave.Enqueue(qQueueMain.Dequeue());
                                            }
                                        }
                                        for (iCount = 0; qQueueSave.Count > 0; iCount++)
                                        {
                                            qQueueMain.Enqueue(qQueueSave.Dequeue());
                                        }
                                        if (iNumDeleted != 0)
                                        {
                                            Console.WriteLine("\n" + iNumDeleted + " value(s) deleted");
                                        }
                                        else
                                        {
                                            Console.WriteLine("\nThere were no values that matched your entry");
                                            Console.WriteLine("If you want to delete something, please enter a value contained in the queue");
                                        }
                                        bValid = true;
                                        break;
                                    case "5":
                                        Console.WriteLine(qQueueMain.Count + " item(s) cleared from queue\n");
                                        stStackMain.Clear();
                                        bValid = true;
                                        break;
                                    case "6":
                                        Console.WriteLine("What value do you want to search for in the queue?");
                                        sUserInput = Console.ReadLine();
                                        swStopWatch.Start();
                                        bFound = qQueueMain.Contains(sUserInput);
                                        swStopWatch.Stop();
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
                                    case "7":
                                        bValid = true;
                                        break;
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
                                    case "1":
                                        Console.WriteLine("\nEnter a string to add to the dictionary");
                                        dDictionaryMain.Add(Console.ReadLine() + " ", dDictionaryMain.Count + 1);
                                        Console.WriteLine("\n" + dDictionaryMain.Count + " item(s) in dictionary\n");
                                        bValid = true;
                                        break;
                                    case "2":
                                        dDictionaryMain.Clear();
                                        for (iCount = 1; iCount <= 2000; iCount++)
                                        {
                                            dDictionaryMain.Add("New Entry " + iCount, dDictionaryMain.Count + 1);
                                        }
                                        Console.WriteLine("\n" + dDictionaryMain.Count + " item(s) in dictionary");
                                        bValid = true;
                                        break;
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
                                    case "4":
                                        Console.WriteLine("What value would you like to delete?");
                                        iDictionaryCount = dDictionaryMain.Count;
                                        dDictionaryMain.Remove(Console.ReadLine());
                                        iNumDeleted = iDictionaryCount = dDictionaryMain.Count;
                                        if (iNumDeleted != 0)
                                        {
                                            Console.WriteLine("\n" + iNumDeleted + " value(s) deleted");
                                        }
                                        else
                                        {
                                            Console.WriteLine("\nThere were no values that matched your entry");
                                            Console.WriteLine("If you want to delete something, please enter a value contained in the dictionary");
                                        }
                                        bValid = true;
                                        break;
                                    case "5":
                                        Console.WriteLine(dDictionaryMain.Count + " item(s) cleared from dictionary\n");
                                        dDictionaryMain.Clear();
                                        bValid = true;
                                        break;
                                    case "6":
                                        Console.WriteLine("What value do you want to search for in the dictionary?");
                                        sUserInput = Console.ReadLine();
                                        swStopWatch.Start();
                                        bFound = dDictionaryMain.ContainsKey(sUserInput);
                                        swStopWatch.Stop();
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
                                    case "7":
                                        bValid = true;
                                        break;
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
                        case "4":
                            bValid = true;
                            break;
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
