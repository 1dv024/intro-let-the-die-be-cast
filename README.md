#Tärningen är kastad!

Du ska följa ”steg för steg”-instruktionen i denna introduktionsuppgift och skapa en konsolapplikation med C# och Visual Studio 2015. Applikationen ska slumpa i det slutna intervallet mellan 100 till 1000 tärningskast och presentera en frekvenstabell över förekomsten av ettor, tvåor, osv.

####Steg 1

Starta Visual Studio 2015.

####Steg 2

Du ska skapa ett projekt för en konsolapplikation med C#, välj därför **File ► New ► Project...**.

####Steg 3

Dialogrutan **New Project** visas.

1. Markera **Visual C#** under **Installed**, **Templates**.
2. Kontrollera så att **.NET Framework 4.5** visas i den nedrullningsbara listrutan.
3. Markera **Console Application**.
4. Vid **Name** skriver du in projektets namn (```DieRollsFrequencyTable```).
5. Ange vid **Location** en lämplig katalog där projektet ska sparas (t.ex. ```C:\Projects```).

####Steg 4

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

####Stegt 5

För att köra applikationen välj menykommandot **Debug ► Start Without Debugging**, eller tryck ner tangentbordkombinationen ```Ctrl + F5```.

>#####Vad händer med källkoden i Program.cs?
>
Källkoden i ```Program.cs``` kompileras till IL-kod (”Intermediate Language”) som placeras i en ny fil, Program.exe, en ”*assembly*”. Vid exekvering av applikationen ansvarar en virtuell maskin kallad CLR (”*Common Language Runtime*”), en central del av dotnetramverket (.NET Framework), för att IL-koden i ”*assemblyn*” ”j*ust-in-time*”-kompileras till maskinkod som sedan exekveras.

####Steg 6

Applikationen körs och ett tomt konsolfönster, förutom texten ```Press any key to continue``` som Visual Studio lagt dit, visas. Stäng konsolfönstret genom att trycka på vilken tangent som helst på tangentbordet. 

*Konsolfönstret*

```
Press any key to continue . . .
```

####Steg 7

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
            // >>> Lägg till kommande två rader. <<<
            int roll = 4;
            Console.WriteLine(roll);
        }
    }
}
```

####Steg 8

Testa applikationen genom att välj menykommandot **Debug ► Start Without Debugging**, eller tryck ner tangentbordkombinationen ```Ctrl + F5```. (Gjorda förändringar sparas automatiskt i samband med att ett projekt exekveras).

*Konsolfönstret*

```
4
Press any key to continue . . .
```

####Steg 9

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

####Steg 10

Kör applikationen flera gånger och konstatera att värden mellan 1 och 6 skrivs ut i konsolfönstren.

####Steg 11

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

####Steg 12

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

####Steg 13

Hur många gånger har du hittills sparat de ändringar du gjort? Inte någon gång? Huuu! Hög tid att klicka på knappen **Save All** som sparar alla öppna filer som har osparade ändringar. Ta för vana att spara ofta, t.ex. efter varje sats. ```Ctrl + S```, som sparar filen som har fokus, ska sitta i ryggmärgen.

####Steg 14

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

####Steg 15

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
                frequncyTable[die.Next(1, 7)]++;
            }

            foreach (int value in frequncyTable)
            {
                Console.WriteLine(value);
            }
        }
    }
}
```
 
####Steg 16

Kör applikationen och konstatera att något som kan vara en frekvenstabell skrivs ut i konsolfönstret.

*Konsolfönstret*

```
Ange antal tärningskast [100-1000]: 87
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
- Presentationen av frekvenstabellen har en del övrigt att önska. Vad betyder 129? Vad betyder 163?

Allvarligaste problemet är första punkten ovan eftersom om användaren matar in något som inte kan tolkas som ett heltal så kraschar applikationen.

####Steg 17

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
                frequncyTable[die.Next(0, 6)]++;
            }

            foreach (int value in frequncyTable)
            {
                Console.WriteLine(value);
            }
        }
    }
}
```

####Steg 18

Testa applikationen och konstatera att applikationen inte längre kraschar.  Det går fortfarande att mata in ett tal som inte är i det slutna intervallet mellan 1 och 100!

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

####Steg 19
####Steg 20
####Steg 21
####Steg 22
####Steg 23
####Steg 24
####Steg 25
####Steg 26
####Steg 27
####Steg 28
####Steg 29
####Steg 30
####Steg 31
