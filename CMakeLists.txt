project(irrlicht LANGUAGES C CXX)
cmake_minimum_required(VERSION 3.16)

# irrlicht dependencies
add_library(lzma irrlicht/source/Irrlicht/lzma/LzmaDec.c)
target_include_directories(lzma PUBLIC 
    "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/irrlicht/source/Irrlicht/lzma>"
    "$<INSTALL_INTERFACE:include>"
)

add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/dependencies/zlib)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/dependencies/libpng)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/dependencies/libjpeg)

add_library(bzip2
    ${CMAKE_CURRENT_LIST_DIR}/dependencies/bzip2-1.0.6/blocksort.c
    ${CMAKE_CURRENT_LIST_DIR}/dependencies/bzip2-1.0.6/huffman.c
    ${CMAKE_CURRENT_LIST_DIR}/dependencies/bzip2-1.0.6/crctable.c
    ${CMAKE_CURRENT_LIST_DIR}/dependencies/bzip2-1.0.6/randtable.c
    ${CMAKE_CURRENT_LIST_DIR}/dependencies/bzip2-1.0.6/compress.c
    ${CMAKE_CURRENT_LIST_DIR}/dependencies/bzip2-1.0.6/decompress.c
    ${CMAKE_CURRENT_LIST_DIR}/dependencies/bzip2-1.0.6/bzlib.c
    ${CMAKE_CURRENT_LIST_DIR}/dependencies/bzip2-1.0.6/bzip2recover.c
)
target_compile_definitions(bzip2 PRIVATE "_FILE_OFFSET_BITS=64")
target_include_directories(bzip2 PUBLIC 
    "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/dependencies/bzip2-1.0.6>"
    "$<INSTALL_INTERFACE:include>"
)

add_library(aesGladman
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/aesGladman/aescrypt.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/aesGladman/aeskey.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/aesGladman/aestab.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/aesGladman/fileenc.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/aesGladman/hmac.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/aesGladman/prng.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/aesGladman/pwd2key.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/aesGladman/sha1.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/aesGladman/sha2.cpp
)
target_include_directories(aesGladman PUBLIC 
    "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/irrlicht/source/Irrlicht/aesGladman>"
    "$<INSTALL_INTERFACE:include>"

    PRIVATE "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/irrlicht/include>"
)

#end dependencies

add_library(Irrlicht
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/C3DSMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CAnimatedMeshHalfLife.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CAnimatedMeshMD2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CAnimatedMeshMD3.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CAnimatedMeshSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CAttributes.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CB3DMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CB3DMeshWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CBillboardSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CBoneSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CBSPMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CBurningShader_Raster_Reference.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CCameraSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CColladaFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CColladaMeshWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CColorConverter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CCSMLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CCubeSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CD3D9Driver.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CD3D9HLSLMaterialRenderer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CD3D9NormalMapRenderer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CD3D9ParallaxMapRenderer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CD3D9RenderTarget.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CD3D9ShaderMaterialRenderer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CD3D9Texture.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CDefaultGUIElementFactory.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CDefaultSceneNodeAnimatorFactory.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CDefaultSceneNodeFactory.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CDepthBuffer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CDMFLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CDummyTransformationSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CEmptySceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CFileList.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CFileSystem.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CFPSCounter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGeometryCreator.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGLXManager.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIButton.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUICheckBox.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIColorSelectDialog.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIComboBox.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIContextMenu.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIEditBox.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIEnvironment.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIFileOpenDialog.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIFont.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIImage.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIImageList.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIInOutFader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIListBox.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIMenu.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIMeshViewer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIMessageBox.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIModalScreen.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIProfiler.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIScrollBar.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUISkin.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUISpinBox.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUISpriteBank.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIStaticText.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUITabControl.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUITable.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIToolBar.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUITreeView.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CGUIWindow.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImage.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderBMP.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderDDS.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderJPG.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderPCX.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderPNG.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderPPM.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderPSD.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderPVR.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderRGB.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderTGA.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageLoaderWAL.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageWriterBMP.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageWriterJPG.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageWriterPCX.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageWriterPNG.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageWriterPPM.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageWriterPSD.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CImageWriterTGA.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CIrrDeviceConsole.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CIrrDeviceFB.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CIrrDeviceLinux.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CIrrDeviceSDL.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CIrrDeviceStub.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CIrrDeviceWin32.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CIrrMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CIrrMeshWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CLightSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CLimitReadFile.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CLMTSMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CLogger.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CLWOMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMD2MeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMD3MeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMemoryFile.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMeshCache.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMeshManipulator.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMeshSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMeshTextureLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMetaTriangleSelector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMountPointReader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMS3DMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CMY3DMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CNPKReader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CNullDriver.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COBJMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COBJMeshWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COCTLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COctreeSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COctreeTriangleSelector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COgreMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COpenGLCacheHandler.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COpenGLDriver.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COpenGLExtensionHandler.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COpenGLNormalMapRenderer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COpenGLParallaxMapRenderer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COpenGLShaderMaterialRenderer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COpenGLSLMaterialRenderer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/COSOperator.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CPakReader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleAnimatedMeshSceneNodeEmitter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleAttractionAffector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleBoxEmitter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleCylinderEmitter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleFadeOutAffector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleGravityAffector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleMeshEmitter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticlePointEmitter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleRingEmitter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleRotationAffector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleScaleAffector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleSphereEmitter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CParticleSystemSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CPLYMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CPLYMeshWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CProfiler.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CQ3LevelMesh.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CQuake3ShaderSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CReadFile.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneCollisionManager.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneLoaderIrr.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneManager.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneNodeAnimatorCameraFPS.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneNodeAnimatorCameraMaya.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneNodeAnimatorCollisionResponse.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneNodeAnimatorDelete.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneNodeAnimatorFlyCircle.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneNodeAnimatorFlyStraight.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneNodeAnimatorFollowSpline.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneNodeAnimatorRotation.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSceneNodeAnimatorTexture.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CShadowVolumeSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSkinnedMesh.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSkyBoxSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSkyDomeSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSMFMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSoftwareDriver2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSoftwareDriver.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSoftwareTexture2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSoftwareTexture.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSphereSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSTLMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CSTLMeshWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTarReader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTerrainSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTerrainTriangleSelector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTextSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRFlat.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRFlatWire.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRGouraud2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRGouraudAlpha2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRGouraudAlphaNoZ2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRGouraud.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRGouraudWire.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTriangleBBSelector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTriangleSelector.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRNormalMap.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRStencilShadow.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureBlend.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureDetailMap2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureFlat.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureFlatWire.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraud2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraudAdd2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraudAdd.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraudAddNoZ2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraudAlpha.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraudAlphaNoZ.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraud.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraudNoZ2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraudNoZ.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraudVertexAlpha2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureGouraudWire.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureLightMap2_Add.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureLightMap2_M1.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureLightMap2_M2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureLightMap2_M4.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureLightMapGouraud2_M4.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CTRTextureWire2.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CVideoModeList.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CVolumeLightSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CWADReader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CWaterSurfaceSceneNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CWGLManager.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CWriteFile.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CXMeshFileLoader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CXMLReader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CXMLWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CZBuffer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/CZipReader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/IBurningShader.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/Irrlicht.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/Irrlicht-gcc.cbp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/irrXML.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/leakHunter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/os.cpp
    ${CMAKE_CURRENT_LIST_DIR}/irrlicht/source/Irrlicht/utf8.cpp
)
target_include_directories(Irrlicht PUBLIC 
    "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/irrlicht/source/Irrlicht>"
    "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/irrlicht/include>"

    "$<INSTALL_INTERFACE:include>"
)
#target_compile_definitions(irrlicht PRIVATE "PNG_THREAD_UNSAFE_OK" "PNG_NO_MMX_CODE" "PNG_NO_MNG_FEATURES")

if(BUILD_SHARED_LIBS)
    set(ZLIB_LIBRARY zlib)
else()
    set(ZLIB_LIBRARY zlibstatic)
endif()

# add opengl dependency
set(OpenGL_GL_PREFERENCE GLVND)
find_package(OpenGL REQUIRED)
set(OpenGL_Targets )

if(OPENGL_opengl_LIBRARY) #GLVND GL
    list(APPEND OpenGL_Targets OpenGL::OpenGL)
    if(OpenGL_GLX_FOUND)
         list(APPEND OpenGL_Targets OpenGL::GLX Xxf86vm)
    endif()
else() #Legacy OpenGL
    list(APPEND OpenGL_Targets OpenGL::GL)
endif()

if(OpenGL_GLU_FOUND)
    list(APPEND OpenGL_Targets OpenGL::GLU)
endif()
# end opengl

target_link_libraries(Irrlicht 
    bzip2 lzma ${ZLIB_LIBRARY} png jpeg aesGladman ${OpenGL_Targets}
) 

# install section

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)



install(TARGETS Irrlicht bzip2 lzma ${ZLIB_LIBRARY} png jpeg aesGladman
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    EXPORT Irrlicht
)
install(DIRECTORY ${CMAKE_SOURCE_DIR}/irrlicht/include DESTINATION ${CMAKE_INSTALL_PREFIX})
install(EXPORT Irrlicht 
    FILE IrrlichtTargets.cmake
    NAMESPACE Irrlicht::
    DESTINATION lib/cmake
)

configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/Config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/IrrlichtConfig.cmake
    INSTALL_DESTINATION lib/cmake
)
install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/IrrlichtConfig.cmake
    DESTINATION lib/cmake
)

#export(TARGETS irrlicht bzip2 lzma ${ZLIB_LIBRARY} png jpeg aesGladman
    #NAMESPACE irrlicht FILE irrlicht-config.cmake)
#export(EXPORT irrlicht NAMESPACE irrlicht FILE irrlicht-config.cmake)
