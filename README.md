Прегледувач на слики
====================


Изработка
=======
Кристијан Цветковиќ
<br/>
121002
<br/>
Факултет за информатички науки и компјутерско инжинерство 2014
<br/>
<br/>
Објаснување на апликацијата
=======
Едноставен прегледувач на слики со неколку интересни функционалности.
<br/>
Овој прегледувач на слики овозможува разгледување на именици со слики на вашиот десктоп или персонален компјутер.
<br/>
Имплементирано е и Full Screen можност, со што можете да ги разгледувате вашите омилени слики на целиот екран 
без тешкотии. Само постоечката слика се чува во меморија, што овозможува брзо прикажување без проблеми!
<br/>
При прикажување на сликите во Fullscreen, овозможено е да се вчитуваат транспарентни за неколку моменти што 
ви помага при брзото менување на боите и фокусот на екранот.
<br/>
Секоја слика може да се ротира и зачува!
<br/>
При десен клик, можете да прикажете Slide Show од вашите слики, кои се менуваат на секои 2 секунди!
<br/>
Доколку не сакате да пребарувате слика која што веќе ја имате на дофат (клик), можете и да ја влечете врз 
прегледувачот на слики и таа автоматски ќе се отвори!

Како се користи?
=======
Користењето на овој прегледувач на слики е многу лесно.
<br/>
При првото стартување на прегледувачот, прикажана ви е стандардната слика на програмата.
<br/>
Можете да ги забележите копчињата во долниот лев агол за навигација на сликите.
<br/>
За да отворите слика, потребно е да кликнете на Open копчето, при што ќе ви се отвори прозорче за
одбирање на слика. При одбирање на сликата, прозорчето се исклучува и се враќате на почетниот екран каде што 
можете да ја забележите вашата слика!
<br/>
Доколку кликнете на копчињата Prev или Next, ќе ви се отвори соодветната слика, претходна или следна.
Доколку наидете на првата слика и кликнете на Prev, прегледувачот ќе ви ја прикаже последната слика од
именикот на слики. Слично можете да забележите, доколку кликнете на Next а ја разгледувате последната слика, 
прегледувачот ќе ве префрли на првата слика од именикот.
<br/>
Во долниот дел од прегледувачот на слики, можете да видите каде ви се наоѓа вашата слика и кои се нејзините 
димензии. Десно од копчињата, прикажан е бројот на слики во именикот каде што ги разгледувате сликите.
При десен клик врз сликата, ќе ви се отвори мени каде што можете да го сторите истото.
<br/>
Доколку кликнете на Previous Image, ќе ви се отвори претходната слика, а доколку кликнете на Next Image, ќе
ви се отвори следната слика. 
Овде ќе забележите дополнителни опции!
<br/>
Прегледувачот на слики ви овозможува да ја поставите моменталната слика како ваша Десктоп позадина!
Имате повеќе опции што ви го овозможуваат тоа, како што се Center, Stretch, Tile, Fit и Fill.
Секоја опција ја поставува сликата за позадина на вашата работна површина на свој уникатен начин!
<br/>
Следна е Slide Show опцијата, која ви овозможува да ги разгледувате вашите слики на цел екран, без да кликате
дополнително. Прегледувачот на слики сам ги отвора следните слики на секои 2 секунди!
<br/>
Следни опции ви се да ја зачувате сликата посебно на вашиот компјутер, како и да ја ротирате по своја желба!
Доколку сакате сами да ги разгледувате сликите на цел екран, кликнете двапати на сликата. Прегледувачот ќе
ви ја отвори сликата каде што ќе можете да ги разгледувате сликите со помош на вашата тастатура, специфично
копчињата за лево и десно!
<br/>
Истото можете да го направите и кога не сте на цел екран. Со користење на Num бројките 4 и 6 (десно на вашата тастатура),
ќе можете да ги менувате сликите лево или десно!

Решение на проблемот
=======
- Патеките до сликите се чуваат во листа од `string` објекти
- Индексот на моменталната слика се чува во `int` променлива
- `bool` променлива која ни кажува дали сме во full screen режим
- две `static readonly int` променливи за default големината на прозорецот
- еден објект од класа `FullScreen` кој ни користи при прикажување на сликите во Full Screen режим
- еден `Bitmap` објект за привремено чување на сликата која што се прикажува

При двоен клик на сликата се стартува функцијата `viewSettings()` која што овозможува моменталната форма
да се прикаже без рабови и на цел екран.

За заменување на позадината на работната површина, искористена е класата `Wallpaper` (готова класа од Microsoft која го користи `User32.dll` за успешно променување на позадината.

Опис на имплементацијата
=======


    private void btnOpen_Click(object sender, EventArgs e)
        {
            // Бидејќи при повик на овој настан се вчитуваат нови патеки до слики,
            // мора претходните да се избришат.
            fileNames.Clear();
            // Прикажува прозорец за вчитување слика и проверува дали враќа OK вредност
            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                try
                {
                    // AddRange Методот ни враќа листа од сите bmp, png, gif и jpg датотеки.
                    // Како аргумент зададен е методот Directory.EnumerateFiles кој враќа само потребни датотеки, 
                    // во овој случај, слики. Како аргументи му се зададени патеката до именикот во кој се наоѓа
                    // сликата која што сакаме да ја видиме, и специфицирано е да разгледува само во тој именик.
                    // За крај, користиме lambda expression која што пребарува во вратените string патеки и 
                    // ги проверува со ToLower() методот бидејќи некогаш сликите се зачувани со екстензија со
                    // големи букви, при што не би ни се додале во листата. Го правиме ова само за екстензии за слики.
                    fileNames.AddRange(Directory.EnumerateFiles(Path.GetDirectoryName(openFileDialog1.FileName), "*.*", SearchOption.TopDirectoryOnly).Where(s => s.ToLower().EndsWith(".png") || s.ToLower().EndsWith(".jpg") || s.ToLower().EndsWith(".bmp") || s.ToLower().EndsWith(".gif")));

                    // Ја сетираме вредноста на индексот за моментална слика на индексот на вчитаната слика во 
                    // листата со методот IndexOf(string FileName) каде што на аргумент го праќаме името на патеката
                    // од openFileDialog прозорецот на вчитаната слика.
                    pCurrentImage = fileNames.IndexOf(openFileDialog1.FileName);
                }
                catch (Exception ioe)
                {
                    // Доколку се случи грешка при отворање на сликата, ја прикажуваме грешката во 
                    // лабелата label1.
                    label1.Text = ioe.Message;
                }
                // Го повикуваме методот ShowCurrentMessage() за да се прикаже сликата
                ShowCurrentImage();
            }
        }


<img src="http://i.imgur.com/cEOX2Iu.png" />
<hr/>
<img src="http://i.imgur.com/aivBDls.png" />
