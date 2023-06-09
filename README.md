[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/LoUfHgXd)
# Magic Marble Run

## Introduction

You have to deal with a *Magic Marble Run*. The following image illustrates how the marbe run works:

![Marble Run](./maze-basic.png)

Someone built a scanner to digitalize such marble runs. The scanner splits up the run into segments. If the incline in a segment is negative, the scanner reports a `>` character. If it is positive, the scanner reports a `<`. Therefore, the run shown above is represented as `>>><<<>>><<<>>`.

However, the our marble runs are magic. At each sink, the run has a *Teleporter*. It teleports the marble to another segment where it continues its journey.

![Magic Marble Run](./maze.png)

The scanner identifies teleporters and add their target indexes in the string (i.e. character array) as a four-digit number. Therefore, the run shown above is represented as `>>>0018<<<>>>0021<<<>>`.

```txt
          1         2
0123456789012345678901
----------------------
>>>0018<<<>>>0021<<<>>
   │         │    ▲  ▲
   │         │    │  │
   └─────────┼────┘  │
             │       │
             └───────┘
```

As you can see, when we ad the teleporters to our magic marble run, the marble can start at the very left of the run and exits at the very right.

## Basic Requirements

Write a C# console application that receives a scanned magic marble run as a commend-line argument. You program has to simulate the marble flow and print the following information:

* How many segments does the marble pass while rolling through the run (i.e. how many `>` or `<` characters do you reach in the scanner output)?
* How often is the marble teleported?

Here are some examples. Note that the first example is the marble run shown above.

| Scanned Run                                              | # of Segments | # of Teleports |
| -------------------------------------------------------- | ------------: | -------------: |
| `>>>0018<<<>>>0021<<<>>`                                 |             6 |              2 |
| `>>>>0031<<<>>>0035<<<<>>>>0021<<>>>>`                   |            11 |              3 |
| `>>>>0042<<>>>>0044<<<>>0053<<<<>>>>0018<<<<>>0028<<<>>` |            13 |              5 |

Here are two longer runs. The first one results in 148 segments and 75 teleports:

```txt
>>>>0419<<<>>>0620<<<<>>0146<<<<>>>>0202<<<<>>>0198<<<>>>>0450<<>>>0643<<<>>>>0045<<<<>>>>0655<<<>>0590<<<<>>>0743<<<>>>0144<<>>>>0028<<<>>>0339<<>>>0356<<<<>>0213<<>>0291<<>>0564<<>>0560<<<<>>0124<<>>>>0395<<<<>>>>0549<<<>>0365<<<>>>0263<<<>>>0401<<<>>>>0182<<<>>>0064<<<>>0282<<>>>0062<<<>>>>0506<<<>>>0108<<>>>0230<<<>>>0043<<>>0688<<<<>>>>0441<<>>>0157<<>>0179<<>>>>0098<<<>>>>0663<<<>>>0336<<<>>>>0623<<<>>0574<<>>>0677<<<<>>>0320<<<<>>>0754<<<>>>0435<<<>>>>0301<<>>>>0250<<<<>>0467<<<<>>>>0410<<<<>>>>0386<<<<>>>0074<<>>>0278<<>>0641<<<<>>0088<<>>>0231<<<>>>>0501<<<<>>0717<<>>>>0018<<<<>>>>0610<<>>>0311<<>>>>0471<<<>>>>0708<<<>>>0522<<>>>>0594<<<>>>0534<<>>>>0481<<<<>>>>0705<<<<>>0260<<<<>>0129<<<>>>>0757<<>>>0368<<<>>0532<<<>>>>0733<<>>0165<<<<>>>
```

The second one results in 559 segments and 275 teleports:

```txt
>>>2685<<<<>>>1422<<<>>>2574<<<>>>>2239<<>>1647<<>>1433<<>>>0995<<>>>>0751<<<<>>>>0816<<>>>0436<<<<>>0646<<>>>0721<<<<>>0609<<<>>>1602<<>>1529<<<>>>>2594<<<>>>>1067<<<>>>>1284<<<<>>>>0368<<>>>>2361<<<<>>>0706<<<>>>1903<<<<>>>>0958<<>>>2101<<>>>>2537<<<>>0472<<>>>>1245<<<<>>>>1170<<<>>1796<<>>1459<<>>>>0784<<<<>>>0284<<<>>0047<<<>>>1874<<<>>>>2041<<<>>1718<<<<>>>0128<<<>>>0339<<>>>>0883<<>>>>2378<<<<>>1758<<<<>>>>2313<<<>>>0594<<<<>>>2553<<<<>>1687<<<>>>0268<<>>>>1423<<<<>>>1462<<>>0536<<<>>>>2077<<<<>>>>0358<<<<>>1213<<>>>2397<<<>>>>0565<<>>>>0445<<>>0455<<<<>>>2120<<<<>>>2457<<>>2223<<<<>>>>0834<<<<>>>>2635<<>>>1842<<<>>>1774<<<<>>>1371<<<<>>>1611<<<>>2488<<>>>1825<<<<>>>>1079<<>>2564<<<<>>>>0680<<<<>>>1884<<<>>0425<<>>0252<<<<>>>>2791<<<<>>>1335<<<>>>>1562<<<<>>>>2232<<<<>>>>1114<<<>>>>1907<<<<>>1794<<<>>>>1539<<>>2765<<<<>>>>0975<<<<>>>0210<<<<>>>>0191<<<>>>2783<<<<>>>0771<<>>1004<<>>>>0814<<<>>>2671<<<>>0966<<>>>2745<<<>>2632<<<<>>>>0869<<<<>>2734<<>>>2201<<>>>0900<<<>>>>0220<<>>>>1976<<>>>1729<<<<>>0312<<<<>>>0274<<>>>1050<<<<>>>>2011<<<<>>>1216<<>>0390<<<<>>2408<<>>1296<<>>>1509<<<<>>0492<<>>2620<<>>>0920<<<<>>0029<<>>>>1853<<>>>0301<<<<>>>>0297<<<<>>1357<<<>>>1036<<<<>>>>0597<<<>>>>1346<<>>>1148<<<>>>>0483<<<<>>>>2088<<<>>>>2140<<>>>1949<<<>>>>2729<<>>1139<<<>>0943<<<>>>1179<<>>>0651<<<>>>2528<<>>>0157<<<>>>0057<<<<>>>>1105<<<<>>0846<<<>>0736<<>>1077<<<>>>>2069<<<>>2171<<>>>>2161<<<>>>0075<<<<>>0514<<>>>>1750<<<<>>1706<<>>>>1657<<>>2261<<<<>>>1815<<<<>>>0625<<<>>0911<<>>>2712<<<<>>>>2656<<<>>>2435<<<<>>1268<<<>>>0738<<<<>>>>1574<<>>>>1680<<<<>>2318<<<>>>>1845<<<>>>2485<<>>1660<<<<>>>>1492<<<<>>>>0109<<<<>>>>2245<<>>>0635<<<>>>>0137<<<<>>>>2213<<<>>2406<<>>0327<<<<>>>0349<<>>>>0857<<<<>>>0090<<>>>>1576<<<<>>>>2500<<<>>0555<<>>>>2032<<<<>>>>1250<<<<>>>1304<<<<>>>2350<<<>>>>1224<<<>>0119<<<>>2754<<<>>>1478<<>>>1543<<<>>1394<<<<>>>0019<<<<>>1816<<<<>>>>0665<<<>>>1930<<>>>>1944<<<<>>>>0667<<<>>>>2334<<<>>2030<<<<>>>0872<<<>>>1121<<<<>>1768<<<<>>>>0223<<>>>>0382<<<>>>>1924<<>>>>2515<<>>>>1586<<<>>>0696<<>>>>1872<<>>1965<<<<>>>0176<<<<>>2290<<>>>>0805<<<>>>>0710<<<<>>>0929<<<>>2172<<<>>>>2602<<<<>>>0414<<<>>>1014<<<<>>>0181<<<>>0896<<>>>>2009<<<>>>2152<<<>>>>0553<<<>>1635<<<<>>>>0155<<<>>0106<<>>1392<<<<>>>>1315<<>>2646<<<>>>2702<<>>>>1514<<<>>>>0378<<>>>>0240<<<>>>>0410<<<<>>>>0781<<<<>>>2271<<<>>>>1184<<<<>>>>2689<<>>>>0078<<<>>>1266<<<>>2443<<>>>>1325<<>>>>1150<<>>1195<<>>1096<<<<>>>1087<<<>>>1034<<>>>2477<<<>>>>1482<<<<>>>>0050<<<>>1017<<<<>>2339<<<<>>>0032<<<>>2059<<<>>>1727<<>>>0523<<>>>>2447<<<>>>1616<<<<>>2587<<>>>1379<<<<>>0578<<>>>>1982<<>>2104<<>>>>0493<<>>>>2524<<>>>>2795<<<>>>2263<<<<>>>2124<<<<>>0526<<<>>>1990<<<<>>>>1402<<<<>>>>2292<<<<>>>>1286<<<<>>>>2192<<<>>>2425<<<<>>>0976<<>>>>1696<<<>>>2381<<<<>>0243<<<<>>>>2582<<>>1443<<<<>>
```

## Advanced Requirements

After carefully analyzing the scanner results, you recognize that the scanner sometimes reports the teleport target index as a *hexadecimal number* (e.g. `0x002b`). Change your program so that it can handle hexadecimal values, too.

Here are some examples. Note that the first example is the marble run shown above.

| Scanned Run                                               | # of Segments | # of Teleports |
| --------------------------------------------------------- | ------------: | -------------: |
| `>>>0x0014<<<>>>0023<<<>>`                                |             6 |              2 |
| `>>0x000c<<<>>>0028<<<<>>0034<<<<>>>`                     |             6 |              3 |
| `>>0020<<>>>>0x0036<<>>>>0037<<>>>0x002a<<<>>>>0017<<<>>` |            11 |              5 |

Here are two longer runs. The first one results in 100 segments and 75 teleports:

```txt
>>>>0613<<>>>>0x0135<<>>>0x031b<<>>>>0x012b<<<<>>>0653<<<<>>>>0x002a<<<>>>>0137<<<>>>0x00ed<<>>>>0829<<<>>>>0x00e8<<<<>>0275<<<>>0513<<<>>>>0022<<>>0462<<<<>>>0364<<<>>>0215<<>>0x01db<<<>>0598<<>>0430<<>>>>0398<<<>>>0x02fc<<>>>0x0184<<<<>>0677<<>>>>0x030e<<>>>0811<<>>>>0x0160<<<<>>>>0815<<<<>>0x02d2<<<>>0195<<<<>>>>0x007d<<<<>>0568<<<>>0127<<<<>>0x00ad<<>>>0x0047<<<<>>>0537<<<>>>0334<<<<>>>>0x029c<<<<>>0265<<>>0647<<>>0412<<>>>0107<<<<>>>>0x00c1<<<<>>>>0x00f7<<<<>>>0x020a<<<>>>>0x0307<<<<>>0x00d2<<>>>>0637<<<>>>>0x011b<<<>>0x0272<<>>>>0x003b<<<<>>0x0052<<<>>0101<<<<>>>0x0013<<>>0x01ee<<<<>>>>0711<<>>>0x002f<<<<>>>0x02f5<<<>>>0584<<>>>>0x02ab<<>>>>0344<<>>0534<<>>>>0x01e1<<<>>>0695<<<<>>>0x0244<<<>>0x0228<<<>>0x02eb<<<<>>>0x01a4<<>>>0x02e0<<>>>0x0092<<>>>>0447<<<<>>>0182<<>>>0x013a<<<<>>0369<<>>>0x009e<<<>>>0x0194<<<<>>
```

The second one results in 416 segments and 275 teleports:

```txt
>>1218<<<>>>>0x0b37<<>>0x032a<<<<>>>0x06fb<<<>>>0x070f<<<<>>0x00b3<<>>>>0x093a<<<>>>0x0022<<>>>1662<<<>>>>0x08ee<<<<>>>>0448<<<>>>>0567<<<>>>>0x057b<<<<>>0917<<>>>>0x04fa<<>>>0x0901<<<>>>>2374<<<<>>0x025c<<>>>>0x0526<<>>>>0x0437<<<<>>>>0193<<>>0x048d<<<>>>>0x0b90<<<<>>>>2627<<>>>0x0040<<>>>>0x0aec<<<>>0x0483<<<<>>>2547<<>>2538<<<<>>>>0x02fa<<<>>0x0bdc<<<<>>0x091e<<<>>>>0x02ee<<<<>>>>1216<<<<>>>>2609<<<>>>2930<<>>>0x0a5a<<>>1623<<<<>>>0x09b6<<<<>>0x01a0<<>>0x017e<<<<>>>>0x0341<<<>>0x068c<<>>>>2325<<<>>1292<<<>>1464<<>>>0x090b<<<<>>0x0681<<<<>>>>0333<<>>>>0153<<<<>>>>0974<<>>>>0x0476<<<<>>2785<<<>>>>0x0734<<<>>>>0x076c<<<<>>>0648<<<>>>>1876<<<>>>0x08b7<<<<>>>2595<<<<>>>0x0726<<<<>>>0346<<<<>>0899<<<>>0x0143<<<>>>0x0831<<<>>>>0x0981<<<>>>>0x0516<<<>>0x008d<<>>1653<<<>>>>2476<<<<>>>1126<<<<>>>0083<<<<>>>0x04a6<<>>>0x0782<<<<>>0x0166<<<<>>>>1305<<<>>>0x04e1<<>>0x07ad<<<<>>>1372<<<<>>>2447<<<>>>>2095<<>>>0279<<<<>>>>1561<<<<>>>0x0b69<<>>0x075e<<>>0x024a<<<>>0x0ab6<<>>>0x0b43<<>>>2464<<>>0x07c8<<>>0872<<>>>0x0605<<<<>>>>2417<<<<>>>0x0663<<>>>0x0106<<<>>>0x02c0<<>>>>2187<<<<>>>0x0852<<<>>>0x05f7<<<>>>>3000<<<>>>0x0ae3<<<<>>0x076e<<>>>>2133<<<<>>>0315<<<<>>>>0x095a<<>>>>0x0454<<<>>0209<<>>>0x00c5<<>>>1085<<<>>>0x071a<<<>>0x0930<<>>2640<<<<>>>>0x01e3<<>>0663<<<<>>>0x05a2<<<>>>>0898<<>>2411<<<<>>>0x0632<<<<>>>0x01bb<<>>>1389<<<<>>>0249<<>>>>1178<<>>0985<<>>0x0420<<>>0x0589<<>>>>0688<<>>0x0b15<<<>>>0046<<<>>>0x0a1e<<>>>>0x02c2<<<<>>>0x0787<<<>>>0291<<<>>>0x069e<<<>>>>1578<<<<>>>0397<<<>>>0x004d<<>>>>1019<<>>>>1937<<<>>2756<<<<>>>0x0313<<<>>>>2271<<>>>2662<<>>>0x06b0<<<<>>>>0x08f7<<<<>>>0772<<<<>>>>0x00a8<<<<>>>0x06f8<<<>>>>0944<<>>2182<<<>>>0x0603<<>>>1798<<<>>0x0a80<<>>>>1861<<<>>>>0x0a88<<<>>>>0x086d<<>>>>0x05e2<<<<>>2169<<>>0x061b<<>>>0x0448<<<<>>0855<<<<>>1486<<<>>>0x064b<<<<>>2754<<<>>1607<<<>>>0x09f9<<<<>>2259<<<>>1755<<>>>0x0af7<<<>>>>2860<<<>>>0501<<<<>>0x0554<<<>>>0656<<<>>>0x02dc<<<<>>>2580<<<<>>>>0x022a<<>>0x07b7<<>>0x0b55<<>>>>1335<<<>>>0240<<<<>>>>0413<<<>>>0x07ea<<>>>>2086<<<>>0x06e7<<<<>>>>0x0241<<<<>>0x03ac<<<>>2241<<<>>0x05af<<<>>2038<<>>>>2070<<<>>2970<<<>>>>0x046b<<>>0x09de<<<<>>0104<<<<>>>2995<<<<>>1741<<>>>0x09d2<<>>>0x01fe<<<<>>>>0x0bc4<<<>>0x03e2<<<>>0x0b0c<<>>0x02d5<<>>>>0x0a7c<<<>>>>2149<<>>>1197<<<<>>0x06d5<<<>>>>2668<<>>>>0x0335<<>>>2911<<<>>2849<<<<>>>1357<<>>>>0009<<>>2387<<<>>>0x04f4<<>>>2711<<<<>>0x0b83<<<>>>>0x007c<<<>>>0x0b29<<<<>>>0x0063<<<>>0x08a0<<<>>>>0022<<>>>0x0896<<<>>1704<<<<>>0x01d0<<<>>0777<<>>0x00e2<<>>>2055<<>>>0886<<<<>>>0x0580<<>>0x09c0<<<>>>>0x0ad5<<>>>0x01a9<<>>0x07e3<<<>>>0x01df<<<<>>2116<<<>>0x05d2<<>>0953<<<<>>>>0x0561<<<>>>>0x0401<<<<>>0x0bd4<<<>>>>1947<<<<>>0x03c5<<>>>>0x0543<<<<>>2282<<<>>0x06b9<<>>>2064<<>>>0x031d<<<<>>>0522<<<>>>>0x034f<<<<>>>>0x07c4<<<>>0681<<<>>1509<<<<>>>0x0595<<>>>2719<<<<>>2220<<<>>2986<<<<>>0x03a1<<<<>>>0592<<<<>>>2937<<<>>>>1004<<<>>2572<<>>>0535<<<<>>>0x07d4<<<<>>0x04ce<<>>>>0x026e<<<>>0519<<<>>>0x0415<<<<>>>>0128<<>>0x0170<<>>0x0737<<<<>>>2472<<>>>0x0114<<>>>0308<<>>>0x04e5<<<>>0628<<<<>>>1061<<<<>>0x0985<<<<>>>>
```

## Even More Advanced Requirements

**Note** that this part of the exercise is much harder than the ones before.

You recognize that the scanner sometimes has read errors. It reports back runs with endless loops in them, i.e. runs where the marble never reaches the exit at the right. Here is an example:

```txt
>>0020<<>>>>0x0016<<>>>>0037<<>>>0x002a<<<>>>>0017<<<>>
```

Write a method `IsValidMarbleRun` that returns `false` if the marble run contains an endless loop. If it does, print a meaningful error message on the screen.
