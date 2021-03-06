---
title: Практическое руководство. Сжатие и извлечение файлов
description: Сжимайте и извлекайте файлы с помощью System.IO.Compression. Ознакомьтесь с примерами использования ZipFile, ZipArchive, ZipArchiveEntry, DeflateStream и GZipStream.
ms.date: 01/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O [.NET], compression
- compression
- compress files
ms.assetid: e9876165-3c60-4c84-a272-513e47acf579
ms.openlocfilehash: ea078099aba3161818844d14af221eb582e7f11b
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188293"
---
# <a name="how-to-compress-and-extract-files"></a>Практическое руководство. Сжатие и извлечение файлов

Пространство имен <xref:System.IO.Compression> предоставляет следующие типы для сжатия и распаковки файлов и потоков. Вы также можете использовать эти типы для чтения и изменения содержимого сжатого файла.

- <xref:System.IO.Compression.ZipFile>
- <xref:System.IO.Compression.ZipArchive>
- <xref:System.IO.Compression.ZipArchiveEntry>
- <xref:System.IO.Compression.DeflateStream>
- <xref:System.IO.Compression.GZipStream>

В примерах ниже показано несколько операций для работы со сжатыми файлами. Для этих примеров требуется добавить в проект следующие пакеты NuGet:

- [System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression);
- [System.IO.Compression.ZipFile](https://www.nuget.org/packages/System.IO.Compression.ZipFile).

Если вы используете .NET Framework, добавьте в проект ссылки на эти две библиотеки:

- `System.IO.Compression`
- `System.IO.Compression.FileSystem`

## <a name="example-1-create-and-extract-a-zip-file"></a>Пример 1: Создание и извлечение ZIP-файла

В следующем примере показано, как создавать и извлекать сжатый файл *.zip* с помощью класса <xref:System.IO.Compression.ZipFile>. Он сжимает содержимое папки в новый *ZIP* -файл и затем извлекает его в новую папку.

Чтобы запустить пример, создайте папку *start* в папке программы и заполните ее файлами для сжатия.

[!code-csharp[System.IO.Compression.ZipFile#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.zipfile/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipFile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.zipfile/vb/program1.vb#1)]

## <a name="example-2-extract-specific-file-extensions"></a>Пример 2: Извлечение файлов с определенными расширениями

В этом примере выполняется итерация по содержимому существующего *ZIP* -файла и извлекаются файлы с расширением *.txt* . Здесь используется класс <xref:System.IO.Compression.ZipArchive> для доступа к ZIP-файлу и класс <xref:System.IO.Compression.ZipArchiveEntry> для проверки отдельных элементов. Метод расширения <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A> для объекта <xref:System.IO.Compression.ZipArchiveEntry> доступен в классе <xref:System.IO.Compression.ZipFileExtensions?displayProperty=nameWithType>.

Чтобы запустить пример, поместите *ZIP* -файл с именем *result.zip* в папку программы. По запросу укажите имя папки для извлечения.

> [!IMPORTANT]
> При распаковке файлов важно убедиться в отсутствии вредоносных путей, которые могут вести за пределы каталога, в который вы извлекаете файлы. Такая атака известна как обход путей. В следующем примере показано, как правильно проверить наличие вредоносных путей и безопасно извлечь файлы.

[!code-csharp[System.IO.Compression.ZipArchive#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchive/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchive/vb/program1.vb#1)]

## <a name="example-3-add-a-file-to-an-existing-zip"></a>Пример 3. Добавление файла в существующий ZIP-файл

В следующем примере используется класс <xref:System.IO.Compression.ZipArchive> для доступа к существующему *ZIP* -файлу и добавления в него файла. Новый файл сжимается при добавлении в существующий ZIP-файл.

[!code-csharp[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/vb/program1.vb#1)]

## <a name="example-4-compress-and-decompress-gz-files"></a>Пример 4. Сжатие и распаковка GZ-файлов

Также вы можете использовать классы <xref:System.IO.Compression.GZipStream> и <xref:System.IO.Compression.DeflateStream> для сжатия и распаковки данных. Они применяют тот же алгоритм сжатия. Вы можете распаковать объекты <xref:System.IO.Compression.GZipStream>, которые записаны в *GZ* -файл, с помощью многих распространенных средств. В следующем примере показано, как использовать класс <xref:System.IO.Compression.GZipStream> для сжатия и распаковки каталога файлов.

[!code-csharp[IO.Compression.GZip1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.Compression.GZip1/CS/gziptest.cs#1)]
[!code-vb[IO.Compression.GZip1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.Compression.GZip1/VB/gziptest.vb#1)]

## <a name="see-also"></a>См. также

- <xref:System.IO.Compression.ZipArchive>  
- <xref:System.IO.Compression.ZipFile>  
- <xref:System.IO.Compression.ZipArchiveEntry>  
- <xref:System.IO.Compression.DeflateStream>  
- <xref:System.IO.Compression.GZipStream>  
- [Файловый и потоковый ввод-вывод](index.md)
