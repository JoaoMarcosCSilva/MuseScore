
add_library(poppler STATIC
   poppler/Annot.cc
   poppler/Array.cc
   poppler/BuiltinFont.cc
   poppler/BuiltinFontTables.cc
   poppler/CachedFile.cc
   poppler/Catalog.cc
   poppler/CharCodeToUnicode.cc
   poppler/CMap.cc
   poppler/DateInfo.cc
   poppler/Decrypt.cc
   poppler/Dict.cc
   poppler/Error.cc
   poppler/FileSpec.cc
   poppler/FontEncodingTables.cc
   poppler/Form.cc
   poppler/FontInfo.cc
   poppler/Function.cc
   poppler/Gfx.cc
   poppler/GfxFont.cc
   poppler/GfxState.cc
   poppler/GlobalParams.cc
   poppler/Hints.cc
   poppler/JArithmeticDecoder.cc
   poppler/JBIG2Stream.cc
   poppler/JPXStream.cc
   poppler/Lexer.cc
   poppler/Linearization.cc
   poppler/Link.cc
   poppler/LocalPDFDocBuilder.cc
   poppler/MarkedContentOutputDev.cc
   poppler/Movie.cc
   poppler/NameToCharCode.cc
   poppler/Object.cc
   poppler/OptionalContent.cc
   poppler/Outline.cc
   poppler/OutputDev.cc
   poppler/Page.cc
   poppler/PageLabelInfo.h
   poppler/PageLabelInfo.cc
   poppler/PageTransition.cc
   poppler/Parser.cc
   poppler/PDFDoc.cc
   poppler/PDFDocEncoding.cc
   poppler/PDFDocFactory.cc
   poppler/PopplerCache.cc
   poppler/PreScanOutputDev.cc
   poppler/ProfileData.cc
   poppler/PSOutputDev.cc
   poppler/PSTokenizer.cc
   poppler/Rendition.cc
	poppler/SecurityHandler.cc
	poppler/SignatureInfo.cc
	poppler/Sound.cc
	poppler/SplashOutputDev.cc
   poppler/StdinCachedFile.cc
   poppler/StdinPDFDocBuilder.cc
   poppler/Stream.cc
   poppler/strtok_r.cpp
	poppler/StructElement.cc
	poppler/StructTreeRoot.cc
	poppler/TextOutputDev.cc
   poppler/UnicodeMap.cc
   poppler/UnicodeTypeTable.cc
	poppler/UTF.cc
	poppler/ViewerPreferences.cc
   poppler/XRef.cc

   goo/FixedPoint.cc
   goo/gfile.cc
   goo/gmem.cc
   goo/gmempp.cc
   goo/GooHash.cc
   goo/GooList.cc
   goo/GooString.cc
   goo/GooTimer.cc
	goo/grandom.cc
   goo/gstrtod.cc
   goo/ImgWriter.cc
   goo/JpegWriter.cc
	goo/NetPBMWriter.cc
	goo/PNGWriter.cc
	goo/TiffWriter.cc
   goo/glibc.cc

   fofi/FoFiBase.cc
   fofi/FoFiEncodings.cc
	fofi/FoFiIdentifier.cc
   fofi/FoFiTrueType.cc
   fofi/FoFiType1.cc
   fofi/FoFiType1C.cc

	splash/Splash.cc
	splash/SplashBitmap.cc
	splash/SplashClip.cc
	splash/SplashFont.cc
	splash/SplashFontEngine.cc
	splash/SplashFontFile.cc
	splash/SplashFontFileID.cc
	splash/SplashFTFont.cc
	splash/SplashFTFontEngine.cc
	splash/SplashFTFontFile.cc
	splash/SplashPath.cc
	splash/SplashPattern.cc
	splash/SplashScreen.cc
	splash/SplashState.cc
	splash/SplashT1Font.cc
	splash/SplashT1FontEngine.cc
	splash/SplashT1FontFile.cc
	splash/SplashXPath.cc
	splash/SplashXPathScanner.cc

	qt5/ArthurOutputDev.cc
	qt5/poppler-annotation.cc
	qt5/poppler-base-converter.cc
	qt5/poppler-document.cc
	qt5/poppler-embeddedfile.cc
	qt5/poppler-fontinfo.cc
	qt5/poppler-form.cc
	qt5/poppler-link-extractor.cc
	qt5/poppler-link.cc
	qt5/poppler-media.cc
	qt5/poppler-movie.cc
	qt5/poppler-optcontent.cc
	qt5/poppler-page-transition.cc
	qt5/poppler-page.cc
	qt5/poppler-pdf-converter.cc
	qt5/poppler-private.cc
	qt5/poppler-ps-converter.cc
	qt5/poppler-qiodeviceoutstream.cc
	qt5/poppler-sound.cc
	qt5/poppler-textbox.cc
   )

if (APPLE)
   set ( POPPLER_COMPILE_FLAGS "-O2 -Wno-unknown-warning-option -Wno-write-strings -ansi -Wnon-virtual-dtor -Woverloaded-virtual -Wno-unused-private-field -Wno-return-stack-address -Wno-shift-negative-value -std=c++11")
else (APPLE)
   if (MINGW)
      set (POPPLER_COMPILE_FLAGS "-O2 -Wall -Wextra -Wno-write-strings -ansi -Wnon-virtual-dtor -Woverloaded-virtual -Wno-unused-parameter -Wno-missing-field-initializers -Wno-unused-but-set-variable -Wno-format -std=c++11")
   else (MINGW)
      if (NOT MSVC)
         set (POPPLER_COMPILE_FLAGS "-O2 -Wno-write-strings -ansi -Wnon-virtual-dtor -Woverloaded-virtual -Wno-unused-parameter -Wno-missing-field-initializers -Wno-unused-but-set-variable -std=c++11")
      else (NOT MSVC)
         # For MSVC:
         # -O2: controls optimization, not compatible with global options
         # -ansi & -std=c++11 -> gloablly set /std:c++14 should take care.
         # -Wno-write-strings    -> ???
         # -Wno-unused-parameter -> Warning C4100: 'identifier' : unreferenced formal parameter
         # -Wnon-virtual-dtor    -> /Wall enabled all warnings, no need to enable particularly (Warning C4265: 'classname': class has virtual functions, but destructor is not virtual\n instances of this class may not be destructed correctly)
         # -Woverloaded-virtual  -> /Wall enabled all warnings, no need to enable particularly
         # -Wno-missing-field-initializers -> ???
         # -Wno-unused-but-set-variable -> Warning C4189: 'identifier': local variable is initialized but not referenced
         set (POPPLER_COMPILE_FLAGS "/wd4065 /wd4100 /wd4121 /wd4127 /wd4189 /wd4244 /wd4245 /wd4310 /wd4255 /wd4267 /wd4309 /wd4334 /wd4456 /wd4458 /wd4459 /wd4701 /wd4702 /wd4703 /wd4706 /wd4805 /wd4996")
      endif (NOT MSVC)
   endif(MINGW)
endif(APPLE)

set_target_properties(poppler
      PROPERTIES
         COMPILE_FLAGS
            ${POPPLER_COMPILE_FLAGS}
      )

include_directories(
        ${PROJECT_SOURCE_DIR}/thirdparty/poppler/goo
	${PROJECT_SOURCE_DIR}/thirdparty/poppler/fofi
	${PROJECT_SOURCE_DIR}/thirdparty/poppler/splash
	${PROJECT_SOURCE_DIR}/thirdparty/poppler/qt5
      )
