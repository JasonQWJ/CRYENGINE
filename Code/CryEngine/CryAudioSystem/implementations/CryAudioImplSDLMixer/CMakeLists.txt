#START-FILE-LIST
# File List auto generated by waf2cmake.py, do not modify manually.

start_sources()
# -- cryaudioimpl.waf_files --
sources_platform(ALL)
add_sources("CryAudioImpl_uber_0.cpp"
	SOURCE_GROUP "Header Files"
		"ATLEntities.h"
		"AudioImpl.h"
		"AudioImplCVars.h"
		"Common.h"
		"GlobalData.h"
		"resource.h"
		"SoundEngine.h"
		"SoundEngineTypes.h"
		"SoundEngineUtil.h"
		"stdafx.h"
	SOURCE_GROUP "Source Files"
		"AudioImpl.cpp"
		"AudioImplCVars.cpp"
		"Common.cpp"
		"CryAudioImpl.cpp"
		"SoundEngineTypes.cpp"
		"SoundEngine.cpp"
)

add_sources("NoUberFile"
	SOURCE_GROUP "Root"
		"stdafx.cpp"
)

end_sources()
#END-FILE-LIST

if(AUDIO_SDL_MIXER)
	CryEngineModule(CryAudioImplSDLMixer FORCE_SHARED_WIN PCH "stdafx.cpp" SOLUTION_FOLDER "CryEngine/Audio/Implementations")
	target_link_libraries(${THIS_PROJECT} PRIVATE
		SDL2
		sdl_mixer_static
		timidity
		native_midi
		flac_static
		libmikmod_static
		libvorbis_static
		libvorbisfile
	)

	if(LINUX OR ANDROID)
		target_link_libraries(${THIS_PROJECT} PRIVATE libmodplug_static)
	endif()

	target_include_directories(${THIS_PROJECT} PRIVATE ../../Common)
else()
	CryFileContainer(CryAudioImplSDLMixer SOLUTION_FOLDER "CryEngine/Audio/Implementations")
endif()
