
# MathTime Professional 2 fonts on TeX Live

MathTime Professional 2 is a set of math fonts that can be used, with 
a text font of your choice, to replace the standard Computer Modern fonts 
in TeX/LaTeX . They were created by Micheal Spivak of 
[Publish Or Perish](http://www.mathpop.com).
They are designed to be most compatible with various Times New Roman families, such as the built in TeX Gyre Termes, but also work well with other families, such as Baskerville.

## Installing MathTime Professional 2

This script was written to install the MathTime fonts
on Linux or maxOS systems running the TeX Live (aka MacTeX) distributions. Unless your Linux or Mac operating system is very old your TeX installation is probably TeX Live.

To install the fonts you first need to 
[acquire a copy of the font files from PCTeX](http://www.pctex.com/mtpro2.html).
They will come in `.zip.tpm` or `.zip` format. 
There is a fee for the complete version; however a free "lite" version is also available. This installer has been tested with both versions.

Next you should download the MTPro2 installer script (version 1.1, April 2016). The easiest thing is to save both the font files and the installer into your Home directory.

Now open a terminal. If you've saved the font files in a location other than your Home directory you will need to `cd` into that directory. Now you must make the installer an executable file by running

    chmod +x ./mtpro2-texlive.sh

Then run the installation procedure by typing

    ./mtpro2-texlive.sh -i [PATH TO FONT FILES]

For example, if you've saved the font files and the installer in the same location the command will be

    ./mtpro2-texlive.sh -i mtp2lite.zip.tpm

The following is the output of a succesful install:

    user@user-laptop-1404:~$ mtpro2-texlive.sh -i mtp2lite.zip.tpm
    Unpacking mtp2lite.zip.tpm.
    [sudo] password for user: 
    Copying files.
    Installing MathTime Professional 2.
      > running texhash
      > updating map references
      > editing updmap.cfg
      > updating TeX Live databases
    TeX Live updated; checking that MTPro2 works...
    Succesfully compiled LaTeX file with MTPro2 included.
    MathTime Professional 2 installed.
    Documentation available at /usr/local/share/texmf/docs/	

If the installation fails you should consult the install log file, at 
`mtpro2-texlive.sh.log`. You can email me at jamespfennell@gmail.com, or post a question on the 
[Tex Stack Exchange site](https://tex.stackexchange.com). If you email me, please attach a copy of the install log.

For instructions on how to use the other features of the installer run

    ./mtpro2-texlive.sh -h

## Using MathTime Professional 2

To use MathTime you must pair it with a text font. MathTime is designed to work well with Times New Roman text fonts, for example TeX Gyre Termes.

I'm a big fan of the Linux Libertine fonts, available through the Latex libertine package. The Libertine fonts are very extensive (they include, for example, small caps) and I think look better than Times.

To use the MathTime Lite version with Libertine you should include the following commands in the header of your LaTeX document:

    \usepackage{libertine}
    \usepackage[T1]{fontenc}
    \usepackage{amsmath}
    \usepackage[lite,subscriptcorrection,slantedGreek,nofontinfo,amsbb,eucal]{mtpro2}

If you have the MathTime Complete version you generally do not need include the     
`amsmath` package, and can take advantage of Times compatible calligraphic and blackboard fonts that are included in the complete version. In this case you can use the following code:

    \usepackage{libertine}
    \usepackage[T1]{fontenc}
    \usepackage[subscriptcorrection,slantedGreek,nofontinfo,mtpcal,mtpfrak,mtphrb]{mtpro2}


For more information on the Latex `mtpro2` package, including
various options available, consult the 
[package documentation](http://www.pctex.com/files/managed/1/1b/mtpro2Abbrev.pdf)


Links:

git clone https://aur.archlinux.org/tex-math-time-pro2-lite.git
cd tex-math-time-pro2-lite
cp /some/path/mtp2lite.zip.tpm
vi PKGBUILD

Edit

# Contributor: orumin <dev@orum.in>

# notice:
#
# BUILD INSTRUCTIONS:
# -------------------
#
# You can download MathTime Pro2 Lite font below:
#
# http://www2.pctex.com/downloads.php?product=MTP2L
#
# if you have done downloaded, mtp2lite.zip.tpm place same as this PKGBUILD directory
# Then, uncomment source and md5sums

pkgname=tex-math-time-pro2-lite
pkgver=1.000
pkgrel=1
pkgdesc="TeX math commercial font (free version)"
url="http://www.pctex.com/mtpro2.html"
license=('custom')
arch=('any')
dpeendes=('texlive-core')
install=mtp2lite.install
source=("mtp2lite.zip.tpm")
md5sums=('278045b67872ffab6767efff3f58c7ad')

package() {
    cd "${srcdir}"

    install -d "${pkgdir}/usr/local/share/"
    install -d "${pkgdir}/usr/share/licenses/${pkgname}"

    install -Dm644 EULA-MTPro2Lite.txt "${pkgdir}/usr/share/licenses/${pkgname}"
    cp -r texmf "${pkgdir}"/usr/local/share/
}
makepkg -si
sudo updmap-sys --enable Map mtpro2.map
https://tex.stackexchange.com/questions/75679/problems-installing-mathtime-professional-2-font-on-texlive
