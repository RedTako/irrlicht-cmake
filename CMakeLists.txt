project(irrlicht LANGUAGES C CXX)
cmake_minimum_required(VERSION 3.16)

# irrlicht dependencies
add_library(lzma irrlicht/source/Irrlicht/lzma/LzmaDec.c)
target_include_directories(lzma PUBLIC 
    "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/irrlicht/source/Irrlicht/lzma>"
    "$<INSTALL_INTERFACE:include>"
)

add_subdirectory(dependencies/zlib)
add_subdirectory(dependencies/libpng)
add_subdirectory(dependencies/libjpeg)

add_library(bzip2
    dependencies/bzip2-1.0.6/blocksort.c
    dependencies/bzip2-1.0.6/huffman.c
    dependencies/bzip2-1.0.6/crctable.c
    dependencies/bzip2-1.0.6/randtable.c
    dependencies/bzip2-1.0.6/compress.c
    dependencies/bzip2-1.0.6/decompress.c
    dependencies/bzip2-1.0.6/bzlib.c
    dependencies/bzip2-1.0.6/bzip2recover.c
)
target_compile_definitions(bzip2 PRIVATE "_FILE_OFFSET_BITS=64")
target_include_directories(bzip2 PUBLIC 
    "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/dependencies/bzip2-1.0.6>"
    "$<INSTALL_INTERFACE:include>"
)

add_library(aesGladman
    irrlicht/source/Irrlicht/aesGladman/aescrypt.cpp
    irrlicht/source/Irrlicht/aesGladman/aeskey.cpp
    irrlicht/source/Irrlicht/aesGladman/aestab.cpp
    irrlicht/source/Irrlicht/aesGladman/fileenc.cpp
    irrlicht/source/Irrlicht/aesGladman/hmac.cpp
    irrlicht/source/Irrlicht/aesGladman/prng.cpp
    irrlicht/source/Irrlicht/aesGladman/pwd2key.cpp
    irrlicht/source/Irrlicht/aesGladman/sha1.cpp
    irrlicht/source/Irrlicht/aesGladman/sha2.cpp
)
target_include_directories(aesGladman PUBLIC 
    "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/irrlicht/source/Irrlicht/aesGladman>"
    "$<INSTALL_INTERFACE:include>"

    PRIVATE "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/irrlicht/include>"
)

#end dependencies

add_library(Irrlicht
    irrlicht/source/Irrlicht/C3DSMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CAnimatedMeshHalfLife.cpp
    irrlicht/source/Irrlicht/CAnimatedMeshMD2.cpp
    irrlicht/source/Irrlicht/CAnimatedMeshMD3.cpp
    irrlicht/source/Irrlicht/CAnimatedMeshSceneNode.cpp
    irrlicht/source/Irrlicht/CAttributes.cpp
    irrlicht/source/Irrlicht/CB3DMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CB3DMeshWriter.cpp
    irrlicht/source/Irrlicht/CBillboardSceneNode.cpp
    irrlicht/source/Irrlicht/CBoneSceneNode.cpp
    irrlicht/source/Irrlicht/CBSPMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CBurningShader_Raster_Reference.cpp
    irrlicht/source/Irrlicht/CCameraSceneNode.cpp
    irrlicht/source/Irrlicht/CColladaFileLoader.cpp
    irrlicht/source/Irrlicht/CColladaMeshWriter.cpp
    irrlicht/source/Irrlicht/CColorConverter.cpp
    irrlicht/source/Irrlicht/CCSMLoader.cpp
    irrlicht/source/Irrlicht/CCubeSceneNode.cpp
    irrlicht/source/Irrlicht/CD3D9Driver.cpp
    irrlicht/source/Irrlicht/CD3D9HLSLMaterialRenderer.cpp
    irrlicht/source/Irrlicht/CD3D9NormalMapRenderer.cpp
    irrlicht/source/Irrlicht/CD3D9ParallaxMapRenderer.cpp
    irrlicht/source/Irrlicht/CD3D9RenderTarget.cpp
    irrlicht/source/Irrlicht/CD3D9ShaderMaterialRenderer.cpp
    irrlicht/source/Irrlicht/CD3D9Texture.cpp
    irrlicht/source/Irrlicht/CDefaultGUIElementFactory.cpp
    irrlicht/source/Irrlicht/CDefaultSceneNodeAnimatorFactory.cpp
    irrlicht/source/Irrlicht/CDefaultSceneNodeFactory.cpp
    irrlicht/source/Irrlicht/CDepthBuffer.cpp
    irrlicht/source/Irrlicht/CDMFLoader.cpp
    irrlicht/source/Irrlicht/CDummyTransformationSceneNode.cpp
    irrlicht/source/Irrlicht/CEmptySceneNode.cpp
    irrlicht/source/Irrlicht/CFileList.cpp
    irrlicht/source/Irrlicht/CFileSystem.cpp
    irrlicht/source/Irrlicht/CFPSCounter.cpp
    irrlicht/source/Irrlicht/CGeometryCreator.cpp
    irrlicht/source/Irrlicht/CGLXManager.cpp
    irrlicht/source/Irrlicht/CGUIButton.cpp
    irrlicht/source/Irrlicht/CGUICheckBox.cpp
    irrlicht/source/Irrlicht/CGUIColorSelectDialog.cpp
    irrlicht/source/Irrlicht/CGUIComboBox.cpp
    irrlicht/source/Irrlicht/CGUIContextMenu.cpp
    irrlicht/source/Irrlicht/CGUIEditBox.cpp
    irrlicht/source/Irrlicht/CGUIEnvironment.cpp
    irrlicht/source/Irrlicht/CGUIFileOpenDialog.cpp
    irrlicht/source/Irrlicht/CGUIFont.cpp
    irrlicht/source/Irrlicht/CGUIImage.cpp
    irrlicht/source/Irrlicht/CGUIImageList.cpp
    irrlicht/source/Irrlicht/CGUIInOutFader.cpp
    irrlicht/source/Irrlicht/CGUIListBox.cpp
    irrlicht/source/Irrlicht/CGUIMenu.cpp
    irrlicht/source/Irrlicht/CGUIMeshViewer.cpp
    irrlicht/source/Irrlicht/CGUIMessageBox.cpp
    irrlicht/source/Irrlicht/CGUIModalScreen.cpp
    irrlicht/source/Irrlicht/CGUIProfiler.cpp
    irrlicht/source/Irrlicht/CGUIScrollBar.cpp
    irrlicht/source/Irrlicht/CGUISkin.cpp
    irrlicht/source/Irrlicht/CGUISpinBox.cpp
    irrlicht/source/Irrlicht/CGUISpriteBank.cpp
    irrlicht/source/Irrlicht/CGUIStaticText.cpp
    irrlicht/source/Irrlicht/CGUITabControl.cpp
    irrlicht/source/Irrlicht/CGUITable.cpp
    irrlicht/source/Irrlicht/CGUIToolBar.cpp
    irrlicht/source/Irrlicht/CGUITreeView.cpp
    irrlicht/source/Irrlicht/CGUIWindow.cpp
    irrlicht/source/Irrlicht/CImage.cpp
    irrlicht/source/Irrlicht/CImageLoaderBMP.cpp
    irrlicht/source/Irrlicht/CImageLoaderDDS.cpp
    irrlicht/source/Irrlicht/CImageLoaderJPG.cpp
    irrlicht/source/Irrlicht/CImageLoaderPCX.cpp
    irrlicht/source/Irrlicht/CImageLoaderPNG.cpp
    irrlicht/source/Irrlicht/CImageLoaderPPM.cpp
    irrlicht/source/Irrlicht/CImageLoaderPSD.cpp
    irrlicht/source/Irrlicht/CImageLoaderPVR.cpp
    irrlicht/source/Irrlicht/CImageLoaderRGB.cpp
    irrlicht/source/Irrlicht/CImageLoaderTGA.cpp
    irrlicht/source/Irrlicht/CImageLoaderWAL.cpp
    irrlicht/source/Irrlicht/CImageWriterBMP.cpp
    irrlicht/source/Irrlicht/CImageWriterJPG.cpp
    irrlicht/source/Irrlicht/CImageWriterPCX.cpp
    irrlicht/source/Irrlicht/CImageWriterPNG.cpp
    irrlicht/source/Irrlicht/CImageWriterPPM.cpp
    irrlicht/source/Irrlicht/CImageWriterPSD.cpp
    irrlicht/source/Irrlicht/CImageWriterTGA.cpp
    irrlicht/source/Irrlicht/CIrrDeviceConsole.cpp
    irrlicht/source/Irrlicht/CIrrDeviceFB.cpp
    irrlicht/source/Irrlicht/CIrrDeviceLinux.cpp
    irrlicht/source/Irrlicht/CIrrDeviceSDL.cpp
    irrlicht/source/Irrlicht/CIrrDeviceStub.cpp
    irrlicht/source/Irrlicht/CIrrDeviceWin32.cpp
    irrlicht/source/Irrlicht/CIrrMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CIrrMeshWriter.cpp
    irrlicht/source/Irrlicht/CLightSceneNode.cpp
    irrlicht/source/Irrlicht/CLimitReadFile.cpp
    irrlicht/source/Irrlicht/CLMTSMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CLogger.cpp
    irrlicht/source/Irrlicht/CLWOMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CMD2MeshFileLoader.cpp
    irrlicht/source/Irrlicht/CMD3MeshFileLoader.cpp
    irrlicht/source/Irrlicht/CMemoryFile.cpp
    irrlicht/source/Irrlicht/CMeshCache.cpp
    irrlicht/source/Irrlicht/CMeshManipulator.cpp
    irrlicht/source/Irrlicht/CMeshSceneNode.cpp
    irrlicht/source/Irrlicht/CMeshTextureLoader.cpp
    irrlicht/source/Irrlicht/CMetaTriangleSelector.cpp
    irrlicht/source/Irrlicht/CMountPointReader.cpp
    irrlicht/source/Irrlicht/CMS3DMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CMY3DMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CNPKReader.cpp
    irrlicht/source/Irrlicht/CNullDriver.cpp
    irrlicht/source/Irrlicht/COBJMeshFileLoader.cpp
    irrlicht/source/Irrlicht/COBJMeshWriter.cpp
    irrlicht/source/Irrlicht/COCTLoader.cpp
    irrlicht/source/Irrlicht/COctreeSceneNode.cpp
    irrlicht/source/Irrlicht/COctreeTriangleSelector.cpp
    irrlicht/source/Irrlicht/COgreMeshFileLoader.cpp
    irrlicht/source/Irrlicht/COpenGLCacheHandler.cpp
    irrlicht/source/Irrlicht/COpenGLDriver.cpp
    irrlicht/source/Irrlicht/COpenGLExtensionHandler.cpp
    irrlicht/source/Irrlicht/COpenGLNormalMapRenderer.cpp
    irrlicht/source/Irrlicht/COpenGLParallaxMapRenderer.cpp
    irrlicht/source/Irrlicht/COpenGLShaderMaterialRenderer.cpp
    irrlicht/source/Irrlicht/COpenGLSLMaterialRenderer.cpp
    irrlicht/source/Irrlicht/COSOperator.cpp
    irrlicht/source/Irrlicht/CPakReader.cpp
    irrlicht/source/Irrlicht/CParticleAnimatedMeshSceneNodeEmitter.cpp
    irrlicht/source/Irrlicht/CParticleAttractionAffector.cpp
    irrlicht/source/Irrlicht/CParticleBoxEmitter.cpp
    irrlicht/source/Irrlicht/CParticleCylinderEmitter.cpp
    irrlicht/source/Irrlicht/CParticleFadeOutAffector.cpp
    irrlicht/source/Irrlicht/CParticleGravityAffector.cpp
    irrlicht/source/Irrlicht/CParticleMeshEmitter.cpp
    irrlicht/source/Irrlicht/CParticlePointEmitter.cpp
    irrlicht/source/Irrlicht/CParticleRingEmitter.cpp
    irrlicht/source/Irrlicht/CParticleRotationAffector.cpp
    irrlicht/source/Irrlicht/CParticleScaleAffector.cpp
    irrlicht/source/Irrlicht/CParticleSphereEmitter.cpp
    irrlicht/source/Irrlicht/CParticleSystemSceneNode.cpp
    irrlicht/source/Irrlicht/CPLYMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CPLYMeshWriter.cpp
    irrlicht/source/Irrlicht/CProfiler.cpp
    irrlicht/source/Irrlicht/CQ3LevelMesh.cpp
    irrlicht/source/Irrlicht/CQuake3ShaderSceneNode.cpp
    irrlicht/source/Irrlicht/CReadFile.cpp
    irrlicht/source/Irrlicht/CSceneCollisionManager.cpp
    irrlicht/source/Irrlicht/CSceneLoaderIrr.cpp
    irrlicht/source/Irrlicht/CSceneManager.cpp
    irrlicht/source/Irrlicht/CSceneNodeAnimatorCameraFPS.cpp
    irrlicht/source/Irrlicht/CSceneNodeAnimatorCameraMaya.cpp
    irrlicht/source/Irrlicht/CSceneNodeAnimatorCollisionResponse.cpp
    irrlicht/source/Irrlicht/CSceneNodeAnimatorDelete.cpp
    irrlicht/source/Irrlicht/CSceneNodeAnimatorFlyCircle.cpp
    irrlicht/source/Irrlicht/CSceneNodeAnimatorFlyStraight.cpp
    irrlicht/source/Irrlicht/CSceneNodeAnimatorFollowSpline.cpp
    irrlicht/source/Irrlicht/CSceneNodeAnimatorRotation.cpp
    irrlicht/source/Irrlicht/CSceneNodeAnimatorTexture.cpp
    irrlicht/source/Irrlicht/CShadowVolumeSceneNode.cpp
    irrlicht/source/Irrlicht/CSkinnedMesh.cpp
    irrlicht/source/Irrlicht/CSkyBoxSceneNode.cpp
    irrlicht/source/Irrlicht/CSkyDomeSceneNode.cpp
    irrlicht/source/Irrlicht/CSMFMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CSoftwareDriver2.cpp
    irrlicht/source/Irrlicht/CSoftwareDriver.cpp
    irrlicht/source/Irrlicht/CSoftwareTexture2.cpp
    irrlicht/source/Irrlicht/CSoftwareTexture.cpp
    irrlicht/source/Irrlicht/CSphereSceneNode.cpp
    irrlicht/source/Irrlicht/CSTLMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CSTLMeshWriter.cpp
    irrlicht/source/Irrlicht/CTarReader.cpp
    irrlicht/source/Irrlicht/CTerrainSceneNode.cpp
    irrlicht/source/Irrlicht/CTerrainTriangleSelector.cpp
    irrlicht/source/Irrlicht/CTextSceneNode.cpp
    irrlicht/source/Irrlicht/CTRFlat.cpp
    irrlicht/source/Irrlicht/CTRFlatWire.cpp
    irrlicht/source/Irrlicht/CTRGouraud2.cpp
    irrlicht/source/Irrlicht/CTRGouraudAlpha2.cpp
    irrlicht/source/Irrlicht/CTRGouraudAlphaNoZ2.cpp
    irrlicht/source/Irrlicht/CTRGouraud.cpp
    irrlicht/source/Irrlicht/CTRGouraudWire.cpp
    irrlicht/source/Irrlicht/CTriangleBBSelector.cpp
    irrlicht/source/Irrlicht/CTriangleSelector.cpp
    irrlicht/source/Irrlicht/CTRNormalMap.cpp
    irrlicht/source/Irrlicht/CTRStencilShadow.cpp
    irrlicht/source/Irrlicht/CTRTextureBlend.cpp
    irrlicht/source/Irrlicht/CTRTextureDetailMap2.cpp
    irrlicht/source/Irrlicht/CTRTextureFlat.cpp
    irrlicht/source/Irrlicht/CTRTextureFlatWire.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraud2.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraudAdd2.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraudAdd.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraudAddNoZ2.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraudAlpha.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraudAlphaNoZ.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraud.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraudNoZ2.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraudNoZ.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraudVertexAlpha2.cpp
    irrlicht/source/Irrlicht/CTRTextureGouraudWire.cpp
    irrlicht/source/Irrlicht/CTRTextureLightMap2_Add.cpp
    irrlicht/source/Irrlicht/CTRTextureLightMap2_M1.cpp
    irrlicht/source/Irrlicht/CTRTextureLightMap2_M2.cpp
    irrlicht/source/Irrlicht/CTRTextureLightMap2_M4.cpp
    irrlicht/source/Irrlicht/CTRTextureLightMapGouraud2_M4.cpp
    irrlicht/source/Irrlicht/CTRTextureWire2.cpp
    irrlicht/source/Irrlicht/CVideoModeList.cpp
    irrlicht/source/Irrlicht/CVolumeLightSceneNode.cpp
    irrlicht/source/Irrlicht/CWADReader.cpp
    irrlicht/source/Irrlicht/CWaterSurfaceSceneNode.cpp
    irrlicht/source/Irrlicht/CWGLManager.cpp
    irrlicht/source/Irrlicht/CWriteFile.cpp
    irrlicht/source/Irrlicht/CXMeshFileLoader.cpp
    irrlicht/source/Irrlicht/CXMLReader.cpp
    irrlicht/source/Irrlicht/CXMLWriter.cpp
    irrlicht/source/Irrlicht/CZBuffer.cpp
    irrlicht/source/Irrlicht/CZipReader.cpp
    irrlicht/source/Irrlicht/IBurningShader.cpp
    irrlicht/source/Irrlicht/Irrlicht.cpp
    irrlicht/source/Irrlicht/Irrlicht-gcc.cbp
    irrlicht/source/Irrlicht/irrXML.cpp
    irrlicht/source/Irrlicht/leakHunter.cpp
    irrlicht/source/Irrlicht/os.cpp
    irrlicht/source/Irrlicht/utf8.cpp
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
