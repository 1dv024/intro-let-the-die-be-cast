## Tärningen är kastad!

>__Denna instruktion gäller Visual Studio 2015 och .NET Framework.__

>__Använder du Visual Studio Code och .NET Core 1.1__ kan du i vissa avseenden följa punkterna nedan, då specikellt de som rör programkod. De punkter som är relaterade till kommandon i Visual Studio 2015 är inte direkt applicerbara i Visual Studio Code.

Du ska följa ”steg för steg”-instruktionen i denna introduktionsuppgift och skapa en konsolapplikation med C# och Visual Studio 2015. Applikationen ska slumpa i det slutna intervallet mellan 100 till 1000 tärningskast och presentera en frekvenstabell över förekomsten av ettor, tvåor, osv.

#### Steg 1

Starta Visual Studio 2015.

#### Steg 2

Du ska skapa ett projekt för en konsolapplikation med C#, välj därför **File ► New ► Project...**.

#### Steg 3

Dialogrutan **New Project** visas.

1. Markera **Visual C#** under **Installed**, **Templates**.
2. Kontrollera så att (minst)  **.NET Framework 4.6.1** visas i den nedrullningsbara listrutan.
3. Markera **Console Application**.
4. Vid **Name** skriver du in projektets namn (```DieRollsFrequencyTable```).
5. Ange vid **Location** en lämplig katalog där projektet ska sparas (t.ex. ```C:\Projects```).

#### Steg 4

Visual Studio skapar ett nytt konsolprojekt som placerats i en egen ”solution” med samma namn som projektet. Det nya projektet innehåller bland annat filen ```Program.cs```.

Filer är organiserade i projekt och ett projekt kan innehålla flera filer som tillsammans utgör applikationen. 

Projekt är organiserade i ”*solutions*”. En ”*solution*” kan innehålla flera projekt. Fönstret **Solution Explorer** innehåller projekt och filer.

Filen ```Program.cs``` innehåller klassen ```Program``` med metoden ```Main``` och därmed är minimikraven uppfyllda för att du nu ska kunna köra applikationen.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

#### Steg 5

För att köra applikationen välj menykommandot **Debug ► Start Without Debugging**, eller tryck ner tangentbordkombinationen ```Ctrl + F5```.

>##### Vad händer med källkoden i Program.cs?
>
Källkoden i ```Program.cs``` kompileras till IL-kod (”Intermediate Language”) som placeras i en ny fil, Program.exe, en ”*assembly*”. Vid exekvering av applikationen ansvarar en virtuell maskin kallad CLR (”*Common Language Runtime*”), en central del av dotnetramverket (.NET Framework), för att IL-koden i ”*assemblyn*” ”j*ust-in-time*”-kompileras till maskinkod som sedan exekveras.

#### Steg 6

Applikationen körs och ett tomt konsolfönster, förutom texten ```Press any key to continue``` som Visual Studio lagt dit, visas. Stäng konsolfönstret genom att trycka på vilken tangent som helst på tangentbordet. 

*Konsolfönstret*

```
Press any key to continue . . .
```

#### Steg 7

Applikationen ska simulera tärningskast. Ett tal mellan 1 och 6 kan representera ett tärningskast. Resultatet av ett tärningskast måste sparas i en variabel vars värde sedan presenteras i konsolfönstret.

1. Deklarera en variabel, med namnet roll, av typen int och initiera den till värdet 4.
1. Presentera variabelns värde.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            int roll = 4;
            Console.WriteLine(roll);
        }
    }
}
```

#### Steg 8

Testa applikationen genom att välj menykommandot **Debug ► Start Without Debugging**, eller tryck ner tangentbordkombinationen ```Ctrl + F5```. (Gjorda förändringar sparas automatiskt i samband med att ett projekt exekveras).

*Konsolfönstret*

```
4
Press any key to continue . . .
```

#### Steg 9

Resultatet av ett tärningskast slumpas inte på något vis av applikationen utan är vad som kallas ”hårkodat” till värdet 4. För att slumpa ett värde i det slutna intervallet mellan 1 och 6 måste ett objekt av typen Random användas.

1. Skapa och initiera en referensvariabel, med namnet die (som betyder tärning på engelska), av typen Random att referera till ett objekt av typen Random.
1. Istället för att tilldela variabeln roll värdet 4 ska variabeln tilldelas värdet som metoden Next() returnerar. I detta fall kommer ```die.Next(1, 7)``` att returnera ett värde av typen int i det slutna intervallet mellan 1 och 6.

**Program.cs**
  
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            Random die = new Random();
            int roll = die.Next(1, 7);

            Console.WriteLine(roll);
        }
    }
}
```

#### Steg 10

Kör applikationen flera gånger och konstatera att värden mellan 1 och 6 skrivs ut i konsolfönstren.

#### Steg 11

Applikationen kan nu simulera ett tärningskast. Kravet är att mellan 100 och 1000 tärningskast ska kunna simuleras. Hur ska applikationen göra för att simulera t.ex. 273 tärningskast?

Det kan enklast göras genom att låta en ”*for*”-sats omsluta satserna som slumpar och skriver ut. (Deklarationerna av variablerna ```die``` och ```roll``` placeras lämpligen innan "*for*"-satsen så att de bara skapas en gång istället för 273 gånger.) 

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            Random die = new Random();
            int roll;

            for (int i = 0; i < 273; i++)
            {
                roll = die.Next(1, 7);
                Console.WriteLine(roll);
            }
        }
    }
}
```

#### Steg 12

Antalet tärningskast är nu ”hårdkodat” till 273. Användaren av applikationen ska kunna ange ett heltal i det slutna intervallet mellan 100 och 1000.

1. Deklarera variabeln ```count```.
1. Skriv ut ledtexten "Ange antalet tärningskast [100-1000]: ".
1. Läs in och tolka heltalet användaren matat in och lagra värdet i ```count```.
1. Ersätt ```273``` med ```count``` i ”*for*”-satsens villkorsuttryck.
 
**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            int count;
            Random die = new Random();
            int roll;

            Console.Write("Ange antal tärningskast [100-1000]: ");
            count = int.Parse(Console.ReadLine());

            for (int i = 0; i < count; i++)
            {
                roll = die.Next(1, 7);
                Console.WriteLine(roll);
            }
        }
    }
}
```

#### Steg 13

Hur många gånger har du hittills sparat de ändringar du gjort? Inte någon gång? Huuu! Hög tid att klicka på knappen **Save All** som sparar alla öppna filer som har osparade ändringar. Ta för vana att spara ofta, t.ex. efter varje sats. ```Ctrl + S```, som sparar filen som har fokus, ska sitta i ryggmärgen.

#### Steg 14

Efter att ett antal förändringar är gjorda är det lämpligt att testa applikationen igen.

*Konsolfönstret*

```
...
3
1
1
6
5
2
1
4
2
1
3
6
3
1
5
2
5
5
2
6
3
2
3
4
Press any key to continue . . .
```

#### Steg 15

Applikationen kan nu simulera av användaren angivet antal tärningskast. Men hur ska en frekvenstabell över tärningskasten kunna skrivas ut? För att kunna skriva ut en frekvenstabell måste applikationen räkna antalet framslumpade ettor, tvåor, o.s.v. En träning har sex sidor varför en variabel med plats för sex värden behövs, en så kallad array.

1. Ersätt satsen som deklarerar variabeln ```roll``` med en sats som skapar referensvariabeln ```frequencyTable```, av typen ```int[]```, och tilldela den en referens till en array med sex element.
1. En array har 0-baserat index, d.v.s. det första elementet har index 0, varför tal i det slutna intervallet mellan 0 och 5 nu måste slumpas fram. Satsen som tilldelar roll ett slumpat värde ska ersättas med en sats där det framslumpade värdet leder till att motsvarande elements värde i arrayen ökas med 1.
1. En ”*foreach*”-sats är lämplig att använda för att skriva ut elementens värden i arrayen.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            int count;
            Random die = new Random();
            int[] frequncyTable = new int[6];

            Console.Write("Ange antal tärningskast [100-1000]: ");
            count = int.Parse(Console.ReadLine());

            for (int i = 0; i < count; i++)
            {
                frequncyTable[die.Next(6)]++;
            }

            foreach (int value in frequncyTable)
            {
                Console.WriteLine(value);
            }
        }
    }
}
```
 
#### Steg 16

Kör applikationen och konstatera att något som kan vara en frekvenstabell skrivs ut i konsolfönstret.

*Konsolfönstret*

```
Ange antal tärningskast [100-1000]: 873
146
142
148
132
153
152
Press any key to continue . . .
```

Applikationen uppfyller nu de löst ställda kraven och en frekvenstabell över ett antal tärningskast skrivs ut. Men hur är det med kvalitéten på användargränssnittet?

- Användaren uppmanas att mata in ett heltal i det slutna intervallet mellan 100 och 1000. Men vad händer om användaren matar in något som inte kan tolkas som ett heltal? Vad händer om användaren matar in t.ex. 13? Ska det gå?
- Presentationen av frekvenstabellen har en del övrigt att önska. Vad betyder 146? Vad betyder 132?

Allvarligaste problemet är första punkten ovan eftersom om användaren matar in något som inte kan tolkas som ett heltal så kraschar applikationen.

#### Steg 17

Eventuella fel i samband med inläsning av antalet tärningskast som ska göras måste hanteras.
Satsen som sköter inläsningen måste ersättas av ”*do-while*”-satsen, som får omsluta satsen som skriver ut ledtexten.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            int count;
            Random die = new Random();
            int[] frequncyTable = new int[6];

            do
            {
                Console.Write("Ange antal tärningskast [100-1000]: ");
            } while (!int.TryParse(Console.ReadLine(), out count)); 

            for (int i = 0; i < count; i++)
            {
                frequncyTable[die.Next(6)]++;
            }

            foreach (int value in frequncyTable)
            {
                Console.WriteLine(value);
            }
        }
    }
}
```

#### Steg 18

Testa applikationen och konstatera att applikationen inte längre kraschar.  Det går fortfarande att mata in ett tal som inte är i det slutna intervallet mellan 100 och 1000!

*Konsolfönstret*

```
Ange antal tärningskast [100-1000]: tvåhundratre
Ange antal tärningskast [100-1000]: 1
0
0
1
0
0
0
Press any key to continue . . .
```

#### Steg 19

I samband med inläsningen måste validering ske av värdet så att det ligger i det slutna intervallet mellan 100 och 1000.

Villkorsuttrycket i ”*do-while*”-satsen måste kompletteras så att det undersöker om det inlästa värdet är större eller lika med 100 och att det är mindre eller lika med 1000.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            int count;
            Random die = new Random();
            int[] frequncyTable = new int[6];

            do
            {
                Console.Write("Ange antal tärningskast [100-1000]: ");
            } while (!(int.TryParse(Console.ReadLine(), out count) &&
                     count >= 100 && 
                     count <= 1000));

            for (int i = 0; i < count; i++)
            {
                frequncyTable[die.Next(6)]++;
            }

            foreach (int value in frequncyTable)
            {
                Console.WriteLine(value);
            }
        }
    }
}
```

#### Steg 20

Vid test av applikationen ska det nu vara omöjligt att mata in något annat än ett heltal i det slutna intervallet mellan 100 och 1000.

*Konsolfönstret*

```
Ange antal tärningskast [100-1000]: 59
Ange antal tärningskast [100-1000]: 1548
Ange antal tärningskast [100-1000]: etthundraåttifem
Ange antal tärningskast [100-1000]: 742
122
126
133
116
125
120
Press any key to continue . . .
```

Den första punkten under steg 16 är nu åtgärdad. Återstår att åtgärda den andra punkten, d.v.s. att låta applikationen presentera frekvenstabellen på ett något bättre sätt så att t.ex. tärningssidan framgår:

```
Ettor:	107
Tvåor:	114
…
Sexor:	113
```

#### Steg 21

Applikationen måste känna till vad tärningssidorna kallas. Lämpligt kan då vara att låta en array innehålla de strängar som beskriver tärningens sidor. Då frekvenstabellen sedan presenteras kan respektive sträng skrivas ut tillsammans med resultatet.

1. Lägg till en sats som skapar referensvariabeln ```facets```, av typen ```string[]```, och initiera den med en array innehållande de sex strängar som var och en beskriver tärningens sidor.
1. Ersätt ”*foreach*”-satsen med en ”*for*”-sats som skriver ut varje tärningssida med tillhörande värde i frekvenstabellen.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            int count;
            Random die = new Random();
            string[] facets = {"Ettor", "Tvåor", "Treor", "Fyror", "Femmor", "Sexor"};
            int[] frequncyTable = new int[6];

            do
            {
                Console.Write("Ange antal tärningskast [100-1000]: ");
            } while (!(int.TryParse(Console.ReadLine(), out count) &&
                     count >= 100 && 
                     count <= 1000));

            for (int i = 0; i < count; i++)
            {
                frequncyTable[die.Next(6)]++;
            }

            for (int i = 0; i < facets.Length; i++)
            {
                Console.WriteLine($"{facets[i]}: {frequncyTable[i]}");
            }
        }
    }
}
```

>Det är inte optimalt med en lösning som kräver synkronisering av två olika arrayer. En bättre lösning kan t.ex. vara att använda en associativ array (”dictionary”), men den konstruktionen får vänta till längre fram i kursen.

#### Steg 22

Kör applikationen på nytt. Nu ska det tydligare framgå hur många ettor, tvåor, o.s.v. som har slumpats fram. Lägg märke till att tabellen är något svår att läsa då en-, tio- och hundratal inte står under varandra.

*Konsolfönstret*

```
Ange antal tärningskast [100-1000]: 742
Ettor: 147
Tvåor: 118
Treor: 109
Fyror: 118
Femmor: 124
Sexor: 126
Press any key to continue . . .
```

#### Steg 23

Värden (strängar, heltal, etc.) som skrivs ut med hjälp av en formatspecificerare kan justeras på olika sätt. Den förändrade ```WrtiteLine```-satsen ser till att tärningssidan vänsterjusteras med en fältbredd på sex tecken, och resultatet högerjusteras med en fältbredd på fyra tecken.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            int count;
            Random die = new Random();
            string[] facets = {"Ettor", "Tvåor", "Treor", "Fyror", "Femmor", "Sexor"};
            int[] frequncyTable = new int[6];

            do
            {
                Console.Write("Ange antal tärningskast [100-1000]: ");
            } while (!(int.TryParse(Console.ReadLine(), out count) &&
                     count >= 100 && 
                     count <= 1000));

            for (int i = 0; i < count; i++)
            {
                frequncyTable[die.Next(6)]++;
            }

            for (int i = 0; i < facets.Length; i++)
            {
                Console.WriteLine($"{facets[i], -6}: {frequncyTable[i], 4}");
            }
        }
    }
}
```

#### Steg 24

En körnng av applikationen visar att den nu beträffande användargränssnittet är acceptabel, men har kanske en hel del övrigt att önska, bl.a. saknas felmeddelande vid felaktig inmatning.

*Konsolfönstret*

```
Ange antal tärningskast [100-1000]: sexhundra
Ange antal tärningskast [100-1000]: 1200
Ange antal tärningskast [100-1000]: 42
Ange antal tärningskast [100-1000]: 600
Ettor :  105
Tvåor :   82
Treor :  131
Fyror :  106
Femmor:   88
Sexor :   88
Press any key to continue . . .
```
 
Applikationen uppfyller nu det löst ställda kraven bättre beträffande användargränssnittet. Men hur är det med kvalitéten beträffande koden?

- All kod är skriven i en och samma metod. Ofta vinner även mindre applikationer på att omstruktureras i flera metoder. Det blir då lättar att förstå och därmed underhålla koden.
- Avsaknaden av kommentarer är total vilket försvårar förståelse av koden.

#### Steg 25

Placera koden som har hand om inläsningen av antal tärningskast som ska simuleras i en separat metod med namnet ```ReadNumberOfRolls()```. Metoden anropas och värdet metoden returnerar lagras i den lokala variabeln ```count```.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            int count;
            Random die = new Random();
            string[] facets = {"Ettor", "Tvåor", "Treor", "Fyror", "Femmor", "Sexor"};
            int[] frequncyTable = new int[6];

            count = ReadNumberOfRolls();

            for (int i = 0; i < count; i++)
            {
                frequncyTable[die.Next(6)]++;
            }

            for (int i = 0; i < facets.Length; i++)
            {
                Console.WriteLine($"{facets[i], -6}: {frequncyTable[i], 4}");
            }
        }

        private static int ReadNumberOfRolls()
        {
            int count;

            do
            {
                Console.Write("Ange antal tärningskast [100-1000]: ");
            } while (!(int.TryParse(Console.ReadLine(), out count) &&
                       count >= 100 &&
                       count <= 1000));

            return count;
        }
    }
}
```

#### Steg 26

Även skapandet av frekvenstabellen och presentationen av den kan omstruktureras i två separata metoder.

Trots att koden fortfarande inte innehåller några kommentarer är den lättare att förstå då metodernas namn har valts med omsorg och beskriver väl vad respektive metod har till uppgift.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    class Program
    {
        static void Main(string[] args)
        {
            int count;
            int[] frequncyTable;

            count = ReadNumberOfRolls();

            frequncyTable = CreateDieRollsFrequencyTable(count);

            ViewFrequencyTable(frequncyTable);
        }

        private static int[] CreateDieRollsFrequencyTable(int count)
        {
            int[] frequncyTable = new int[6];
            Random die = new Random();

            for (int i = 0; i < count; i++)
            {
                frequncyTable[die.Next(6)]++;
            }

            return frequncyTable;
        }

        private static int ReadNumberOfRolls()
        {
            int count;

            do
            {
                Console.Write("Ange antal tärningskast [100-1000]: ");
            } while (!(int.TryParse(Console.ReadLine(), out count) &&
                       count >= 100 &&
                       count <= 1000));

            return count;
        }

        private static void ViewFrequencyTable(int[] frequncyTable)
        {
            string[] facets = { "Ettor", "Tvåor", "Treor", "Fyror", "Femmor", "Sexor" };

            for (int i = 0; i < facets.Length; i++)
            {
                Console.WriteLine($"{facets[i],-6}: {frequncyTable[i],4}");
            }
        }
    }
}
```

#### Steg 27

Då användaren råkar mata in något som inte kan tolkas som ett heltal i det slutna intervallet mellan 100 och 1000 visas inget felmeddelande. Metoden ReadNumberOfRolls() måste skrivas om så att så sker.

**Program.cs - ReadNumberOfRolls**

```csharp
        private static int ReadNumberOfRolls()
        {
            int count;

            while (true)
            {
                try
                {
                    Console.Write("Ange antal tärningskast [100-1000]: ");
                    count = int.Parse(Console.ReadLine());
                    if (!(count >= 100 && count <= 1000))
                    {
                        throw new ApplicationException();
                    }

                    return count;
                }
                catch (Exception)
                {
                    Console.BackgroundColor = ConsoleColor.Red;
                    Console.ForegroundColor = ConsoleColor.White;
                    Console.WriteLine("\nFEL! Ange ett heltal mellan 100 och 1000.\n");
                    Console.ResetColor();
                }
            }
        }
```

#### Steg 28

Kör applikationen och att mata in några felaktiga värden. Felmeddelande visas då användaren matar in något som inte kan tolkas som ett heltal i det slutna intervallet mellan 100 och 1000.

*Konsolfönstret*

```
Ange antal tärningskast [100-1000]: tvåhundra

FEL! Ange ett heltal mellan 100 och 1000.

Ange antal tärningskast [100-1000]: 42

FEL! Ange ett heltal mellan 100 och 1000.

Ange antal tärningskast [100-1000]: 1300

FEL! Ange ett heltal mellan 100 och 1000.

Ange antal tärningskast [100-1000]: 240
Ettor :   38
Tvåor :   40
Treor :   38
Fyror :   36
Femmor:   43
Sexor :   45
Press any key to continue . . .
```

#### Steg 29

Presentationen av frekvenstabellen behöver åtgärdas så den liknar en tabell.

**Program.cs - ViewFrequencyTable**

```csharp
        private static void ViewFrequencyTable(int[] frequncyTable)
        {
            string[] facets = { "Ettor", "Tvåor", "Treor", "Fyror", "Femmor", "Sexor" };

            Console.BackgroundColor = ConsoleColor.Blue;
            Console.ForegroundColor = ConsoleColor.White;
            Console.WriteLine("\n----------------");
            Console.WriteLine(" Frekvenstabell ");
            Console.WriteLine("----------------");
            Console.ResetColor();
            for (int i = 0; i < facets.Length; i++)
            {
                Console.WriteLine($" {facets[i],-7} | {frequncyTable[i],4}");
                Console.WriteLine("----------------");
            }
        }
```

#### Steg 30

Kör applikationen och verifiera att frekvenstabellen nu påminner mer om en tabell än tidigare.

*Konsolfönstret*

```
Ange antal tärningskast [100-1000]: 600

----------------
 Frekvenstabell
----------------
 Ettor   |  110
----------------
 Tvåor   |  106
----------------
 Treor   |  112
----------------
 Fyror   |   97
----------------
 Femmor  |   77
----------------
 Sexor   |   98
----------------
Press any key to continue . . .
```

#### Steg 31

Kod ska alltid dokumenteras. Nedan visar hur källkoden blir enklare att förstår när den kompletterats med kommentarer, vilka självklart ska skrivas samtidigt som koden skrivs och inte efter att all kod skrivits klart.

**Program.cs**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DieRollsFrequencyTable
{
    /// <summary>
    /// Applikationen simulerar tärningskast och presenterar utfallet i 
    /// form av en frekvenstabell.
    /// </summary>
    class Program
    {
        /// <summary>
        /// Startpunkt för applikationen.
        /// </summary>
        /// <param name="args">Argument som kan skickas till applikationen (används 
        /// inte).</param>
        static void Main(string[] args)
        {
            // Deklarerar lokala variabler.
            int count;
            int[] frequncyTable;

            // Läser in hur många tärningskast som ska simuleras då
            // en frekvenstabell över tärningskast skapas och presenteras.
            count = ReadNumberOfRolls();

            frequncyTable = CreateDieRollsFrequencyTable(count);

            ViewFrequencyTable(frequncyTable);
        }

        /// <summary>
        /// Simulerar tärningskast, skapar och returnerar frekvenstabell över utfallet.
        /// </summary>
        /// <param name="count">Antal tärningskast att simulera.</param>
        /// <returns>Array innehållande frekvenstabell över simulerade 
        /// tärningskast.</returns>
        private static int[] CreateDieRollsFrequencyTable(int count)
        {
            // Deklarerar lokala variabler.
            int[] frequncyTable = new int[6];
            Random die = new Random();

            // Slumpar tärningskast och uppdaterar frekvenstabellen som därefter 
            // returneras.
            for (int i = 0; i < count; i++)
            {
                frequncyTable[die.Next(6)]++;
            }

            return frequncyTable;
        }

        /// <summary>
        /// Efterfrågar, läser in och returnerar antalet tärningskast som ska simuleras.
        /// </summary>
        /// <returns>Antal tärningskast.</returns>
        private static int ReadNumberOfRolls()
        {
            // Deklarerar lokala variabler.
            int count;

            // Läser in och returnerar ett heltal mellan 100 och 1000.
            while (true)
            {
                try
                {
                    Console.Write("Ange antal tärningskast [100-1000]: ");
                    count = int.Parse(Console.ReadLine());
                    if (count < 100 || count > 1000)
                    {
                        throw new ApplicationException();
                    }

                    return count;
                }
                catch (Exception)
                {
                    Console.BackgroundColor = ConsoleColor.Red;
                    Console.ForegroundColor = ConsoleColor.White;
                    Console.WriteLine("\nFEL! Ange ett heltal mellan 100 och 1000.\n");
                    Console.ResetColor();
                }
            }
        }

        /// <summary>
        /// Presenterar en frekvenstabell över tärningskast.
        /// </summary>
        /// <param name="frequncyTable">Referens till frekvenstabell i form av en array
        /// innehållade utfallet av tärningskast.</param>
        private static void ViewFrequencyTable(int[] frequncyTable)
        {
            // Deklarerar lokal variabel.
            string[] facets = { "Ettor", "Tvåor", "Treor", "Fyror", "Femmor", "Sexor" };

            // Går igenom tärningssida för tärningssida och skriver ut tärningssidans 
            // namn samt antalet gånger sidan "kommit upp" vid ett tärningskast. 
            Console.BackgroundColor = ConsoleColor.Blue;
            Console.ForegroundColor = ConsoleColor.White;
            Console.WriteLine("\n----------------");
            Console.WriteLine(" Frekvenstabell ");
            Console.WriteLine("----------------");
            Console.ResetColor();
            for (int i = 0; i < facets.Length; i++)
            {
                Console.WriteLine($" {facets[i],-7} | {frequncyTable[i],4}");
                Console.WriteLine("----------------");
            }
        }
    }
}
```
