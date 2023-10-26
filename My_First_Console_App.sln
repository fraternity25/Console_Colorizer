/*using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;*/

using System;
using System.Collections.Generic;
using System.Linq;
using System.Windows.Forms; // Import the Windows Forms namespace

/*  TO - DO LIST:
 *  1) USE "(ConsoleColor) 9" FOR COMMENT LINES AND CHAR LITERALS
 *  2) USE "(ConsoleColor) 4" FOR SYMBOLS
 *  3) USE "(ConsoleColor) 6" FOR STRING LITERALS
 *  4) USE "ConsoleColor.Cyan" FOR NAME HOLDERS (#...#)
 *  5) fix going back to the previous lines last collumn problem
 *  6) Handle character inserting
 *  7) Handle mouse input 
 */
namespace My_Console_Colorizer
{
    internal class Program
    {
        private static List<string> keywords = new List<string>();
        private static List<string> functions = new List<string>();
        private static List<string> currentInput = new List<string>();

        [STAThread]
        static void Main(string[] args)
        {
            ConsoleKeyInfo key = new ConsoleKeyInfo(); // Initialize key with a default value
            int line_collumn = 0;
            int index = 0;
            int lastSpaceIndex = 0;
            string lastWord = "";
            string name = "huso";
            string currentCode = "";
            string pastedText = ""; // To store pasted text with CTRL + V
            char[] symbols = { ' ', '\t', '(', ')', '[', ']', '{', '}', '&', '#', '<', '>', '=', '!', '|', ';', ':', '.', ',', '*', '+', '-', '/', '%', '^', '\\', '\"', '\'', '?', '`', '~', '@', '$' };
            bool continue_condition = false;
            bool string_copied = false;
            /*Console.SetBufferSize(164, 40);
            Console.SetWindowSize(164, 40);*/
            Console.WriteLine($"{Console.BufferWidth}");
            Console.WriteLine($"{Console.WindowWidth}");
            Console.WriteLine($"Welcome {name}");
            Console.WriteLine("Type your code. Type 'out;' to exit.");

            // Add some initial keywords
            AddKeyword("using");
            AddKeyword("namespace");
            AddKeyword("class");
            AddKeyword("static");
            AddKeyword("typedef");
            AddKeyword("struct");
            AddKeyword("const");
            AddKeyword("void");
            AddKeyword("int");
            AddKeyword("float");
            AddKeyword("double");
            AddKeyword("char");
            AddKeyword("string");
            AddKeyword("sıze_t");
            AddKeyword("pointer");
            AddKeyword("list");
            AddKeyword("Console");
            AddKeyword("WriteLine");
            AddKeyword("public");
            AddKeyword("from");
            AddKeyword("import");
            AddKeyword("if");
            AddKeyword("else if");
            AddKeyword("else");
            AddKeyword("for");
            AddKeyword("while");
            AddKeyword("with");
            AddKeyword("def");
            AddKeyword("return");
            AddKeyword("pass");
            AddKeyword("try");
            AddKeyword("except");
            AddKeyword("finally");
            AddKeyword("in");
            AddKeyword("is");
            AddKeyword("as");
            AddKeyword("none");
            AddKeyword("NULL");
            AddKeyword("or");
            AddKeyword("and");
            AddKeyword("exit");

            AddFunction("text");
            AddFunction("create");
            AddFunction("process");
            AddFunction("take");
            AddFunction("range");
            AddFunction("search");

            while (true)
            {
                if(string_copied == false)
                {
                    key = Console.ReadKey(true);
                }
                else
                {
                    Console.Write($"index = {index} ");
                    index++;
                    key = new ConsoleKeyInfo(pastedText[index], key.Key, false, false, false);
                    //currentInput.AddRange(pastedText.Select(c => c.ToString()));
                }
                line_collumn++;

                /*if (key.Key == ConsoleKey.C && (key.Modifiers & ConsoleModifiers.Control) != 0)
                {
                    pastedText = Clipboard.GetText(); // Use Clipboard.GetText from System.Windows.Forms to capture the pasted text
                                                      // Trim trailing spaces from the pasted text
                    pastedText = TrimTrailingSpaces(pastedText);

                    // Insert the trimmed text at the cursor position
                    int cursorLeft = Console.CursorLeft;
                    int cursorTop = Console.CursorTop;
                    Console.Write(pastedText);
                    Console.SetCursorPosition(cursorLeft, cursorTop);
                    currentInput.AddRange(pastedText.Select(c => c.ToString()));
                    continue;
                }*/
                if (key.Key == ConsoleKey.Enter)
                {
                    Console.WriteLine();
                    currentInput.Clear();
                    lastSpaceIndex = line_collumn - 1;
                    line_collumn = 0;
                    continue;
                }
                else if (key.Key == ConsoleKey.LeftArrow)
                {
                    line_collumn -= 2;
                    if (line_collumn >= 0)
                    {
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                    }
                    else
                    {
                        line_collumn = 0;
                    }
                    continue;
                }
                else if (key.Key == ConsoleKey.RightArrow)
                {
                    if (line_collumn < currentInput.Count + 1)
                    {
                        Console.SetCursorPosition(Console.CursorLeft + 1, Console.CursorTop);
                    }
                    else
                    {
                        line_collumn -= 1;
                    }
                    continue;
                }
                else
                {
                    if (key.Key == ConsoleKey.Backspace)
                    {
                        line_collumn -= 2;
                        if (line_collumn >= 0)
                        {
                            if (currentInput.Count > 0)
                            {
                                currentInput.RemoveAt(currentInput.Count - 1);
                            }
                            Console.Write("\b \b"); // Clear the character and move cursor back
                            currentCode = string.Join("", currentInput);
                            /*if (currentCode.EndsWith("out;"))
                            {
                                break; // Exit the loop
                            }*/
                        }
                        else if (line_collumn < 0)
                        {
                            line_collumn = 0;
                            continue;
                            //go back to the previous lines last collumn
                        }
                    }
                    else if (key.Key != ConsoleKey.Backspace)
                    {
                        if ((key.Modifiers & ConsoleModifiers.Control) != 0)
                        {
                            Console.Write("Opened for copying. press V to copy >>>>>>>>>>>>>>>>>>>>>> ");
                            ConsoleKeyInfo second_key = Console.ReadKey(true);
                            if (second_key.KeyChar == 'v' /*second_key.Key == ConsoleKey.V*/)
                            {
                                Console.Write("copied\n");
                                pastedText = /*GetClipboardData();*/ Clipboard.GetText();
                                pastedText = TrimTrailingSpaces(pastedText);
                                string_copied = true;
                                //Console.Write($"pastedText = {pastedText}1");
                            }
                            else
                            {
                                Console.Write("returned\n");
                            }
                            //currentInput.AddRange(pastedText.Select(c => c.ToString()));
                            continue;
                        }
                        else if(/*line_collumn < Console.BufferWidth - 1 &&*/ line_collumn < Console.WindowWidth - 2) 
                        {
                            if (key.Key == ConsoleKey.Spacebar)
                            {
                                Console.SetCursorPosition(Console.CursorLeft + 1, Console.CursorTop);
                                currentInput.Add(key.KeyChar.ToString());
                            }
                            else if (key.Key == ConsoleKey.Tab)
                            {
                                if (/*line_collumn < Console.BufferWidth - 1 &&*/ line_collumn < Console.WindowWidth - 5)
                                {
                                    Console.SetCursorPosition(Console.CursorLeft + 4, Console.CursorTop);
                                    for (int i = 0; i < 4; i++)
                                    {
                                        currentInput.Add(" ");
                                    }
                                    line_collumn += 3;
                                }
                                else
                                {
                                    Console.WriteLine(key.KeyChar);
                                    currentInput.Clear();
                                    lastSpaceIndex = line_collumn - 1;
                                    line_collumn = 0;
                                    continue;
                                }
                            }
                            else
                            {
                                currentInput.Add(key.KeyChar.ToString());
                            }

                            currentCode = string.Join("", currentInput);
                            //Console.Write($"\n{currentCode}1\n");
                            /*if (currentCode.EndsWith("out;"))
                            {
                                break; // Exit the loop
                            }*/
                        }
                        else if(/*line_collumn >= Console.BufferWidth - 1 ||*/ line_collumn >= Console.WindowWidth - 2) 
                        {
                            Console.WriteLine(key.KeyChar);
                            currentInput.Clear();
                            lastSpaceIndex = line_collumn - 1;
                            line_collumn = 0;
                            continue;
                        }


                         for (int i = 0; i < 32; i++)
                         {
                             if ((lastSpaceIndex = currentCode.LastIndexOf(symbols[i])) != -1)
                             {
                                 lastWord = currentCode.Substring(lastSpaceIndex + 1);
                                 currentInput.Clear();
                                 if (key.Key != ConsoleKey.Spacebar && key.Key != ConsoleKey.Tab)
                                 {
                                     Console.ForegroundColor = ConsoleColor.Red;
                                     Console.Write(key.KeyChar);
                                 }
                                 continue_condition = true;
                                 break;
                             }
                             else if (i == 31)
                             {
                                 lastWord = currentCode;
                                 if (key.Key != ConsoleKey.Backspace)
                                 {
                                     Console.Write($"{key.KeyChar}");
                                 }
                                 continue_condition = false;
                                 break;
                             }
                         }
                         if (continue_condition == true)
                         {
                             continue;
                         }
                    }
                    for (int i = 0; i < lastWord.Length; i++)
                    {
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                    }
                    if (IsKeyword(lastWord))
                    {
                        for (int i = 0; i < lastWord.Length; i++)
                        {
                            Console.ForegroundColor = (ConsoleColor)2; // Keyword color
                            Console.Write(lastWord[i]);
                        }
                    }
                    else if (IsFunction(lastWord))
                    {
                        for (int i = 0; i < lastWord.Length; i++)
                        {
                            Console.ForegroundColor = ConsoleColor.Yellow; // Function color
                            Console.Write(lastWord[i]);
                        }
                    }
                    else
                    {
                        for (int i = 0; i < lastWord.Length; i++)
                        {
                            Console.ForegroundColor = (ConsoleColor)11;
                            Console.Write(lastWord[i]);
                        }
                    }
                }
            }
            pastedText = string.Empty;
            //Console.ResetColor();
        }

        private static string TrimTrailingSpaces(string text)
        {
            return text.TrimEnd();
        }

        private static void AddKeyword(string keyword)
        {
            keywords.Add(keyword);
        }

        private static void AddFunction(string function)
        {
            functions.Add(function);
        }

        private static bool IsKeyword(string input)
        {
            return keywords.Contains(input);
        }

        private static bool IsFunction(string input)
        {
            return functions.Contains(input);
        }
    }
}

