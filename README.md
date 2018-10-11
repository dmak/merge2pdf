# Merge2PDF

[![Build Status](https://travis-ci.org/dmak/merge2pdf.svg)](https://travis-ci.org/dmak/merge2pdf)
[![Coverage Status](https://coveralls.io/repos/github/dmak/merge2pdf/badge.svg?branch=master)](https://coveralls.io/github/dmak/merge2pdf?branch=master)

If you like this utility, please give in a star in GutHub! Report the issues to [bugtracker](https://github.com/dmak/merge2pdf/issues/).

## Description

This utility allows one to "convert" JPEG to PDF without recompression. More generally, it combines a sequence of PDF, JPEG, TIFF, PNG images into one PDF.  

The code was originally posted [here](https://stackoverflow.com/questions/46664134/merge-pdf-documents-and-images-into-one-pdf), and later evolved into a more powerful utility. 

The question about JPEG-to-PDF conversion was asked several times (see [here](https://askubuntu.com/questions/246647/jpeg-files-to-pdf)), however it is known that [GraphicsMagick](http://www.graphicsmagick.org/) uses [GhostScript](https://www.ghostscript.com/) under the hood, which performs image decompression and then compression (check [this answer comments](https://askubuntu.com/a/473674/164142)) hence `gm convert image.jpg image.pdf` does not fit.

I have done my research and examined PDFs generated by several online services.

These do not perform recompression, but they are online services or commercial products:

*  http://convert-my-image.com/ – based on [iText PDF 5.3.0](https://itextpdf.com/)
*  https://www.pdfpro.co/ – uses [BCL easyPDF](http://www.pdfonline.com/easypdf/)

These perform recompression:

* https://www.freepdfconvert.com/jpg-pdf
* http://jpg2pdf.com/
* http://www.jpgtopdf.com/

Further, [`pdftk`](http://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/ ) and [`qpdf`](http://qpdf.sourceforge.net/files/qpdf-manual.html) only take PDF as input, not images.

## Usage

`java -jar merge2pdf-1.0.jar [-dpi|-A4] one.pdf [two.jpg three.png ...] out.pdf`

<table>
<tr>
	<th>Option</th>
	<th>Comment</th>
</tr>
<tr>
	<td><tt>-dpi</tt></td>
	<td>If image metainformation provides DPI, then scale the image down, namely to <tt>72 / image_DPI × 100%</tt>, where 72 DPI is a standard PDF DPI. This is necessary in case one needs to merge images with different DPI so that they are represented on the same scale in resulting PDF.</td>
</tr>
<tr>
	<td><tt>-An</tt>, e.g. <tt>-A3</tt>, <tt>-A4</tt>, <tt>-A5</tt>, ...</td>
	<td>Scale the image down to fit the given page size (A3, A4, ...). If this options is provided, then `-dpi` is implicitly enabled. Also auto-rotation is applied, i.e. if image width is bigger than height and the image does not fit the portrait-oriented page, page orientation is set to landscape and then the image is scaled down (if necessary).</td>
</tr>
</table>

## Development / Contribution

Please follow [Contribution section](https://github.com/dmak/jaxb-xew-plugin#contribution). 

## License

The whole project is licensed under [GPLv3](https://gnu.org/licenses/gpl.html) (or any later version).
