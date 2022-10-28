# Руководство по wdiff (Перевод)

`texi2any` утилита входящая в состав пакета [`texinfo`](https://www.gnu.org/software/texinfo/).

Протестировано на версии:

```
texi2any --version
texi2any (GNU texinfo) 6.8

Copyright (C) 2021 Free Software Foundation, Inc.
Лицензия GPLv3+: GNU GPL версии 3 или новее <http://gnu.org/licenses/gpl.html>
Это свободное ПО: вы можете продавать и распространять его.
Нет НИКАКИХ ГАРАНТИЙ до степени, разрешённой законом.
```

Сборка html (проходит нормально, страницы отображаются):

```
texi2any --html wdiff.texi
```

Сборка в docbook:

```
texi2any --docbook wdiff.texi
```

21-страничная [Pdf-версия](https://www.gnu.org/software/wdiff/manual/wdiff.pdf) руководства на английском.

## TODO

- [ ] Получить красивую pdf на русском.

## Описание проблемы

Прямой подход к генерации pdf с переводом не работает:

```
texi2pdf wdiff.texi
```

Возможные варианты:

1. Самый простой и самый сложный одновременно:
   
   Использование [локализиции Sergei Golovan](https://github.com/sgolovan/rustexinfo)

   [Информация по шрифтам](https://blog.sandipb.net/2009/02/12/getting-more-printable-pdfs-from-texinfo-manuals/)

   [Модификация шрифтов от GNU press](https://cvs.savannah.nongnu.org/viewvc/gnupress/gnupress/texpress/)

   Сложность заключается в том что генерация pdf происходит без генерации tex-файлов, вторая проблема в использовании кодировки utf-8 - возможно стоит использовать XeTeX (Unicode-based TeX).

2. texi -> docbook -> (pandoc?) -> TeX/LaTex -> pdf
   
   Выбор выходного формата для texi2any (по умолчанию Info):

   *  --docbook                      выводить в формате DocBook XML, а не Info
   *  --html                         выводить в формате HTML, а не Info
   *  --plaintext                    выводить простой текст, а не Info
   *  --xml                          выводить в формате Texinfo XML, а не в Info
   *  --dvi, --dvipdf, --ps, --pdf   вызывать texi2dvi для генерации вывода
                                     после проверки корректности ФАЙЛА-TEXINFO

3. texi -> ([texi2roff](https://www.ctan.org/pkg/texi2roff)) -> groff -> pdf



