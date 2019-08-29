compilled sources from https://github.com/egorovandreyrm/libssh_android_build_scripts with the following config:

API_LEVEL=21

boring ssl cmake:

cmake -DANDROID_ABI=${ANDROID_API} \
      -DCMAKE_TOOLCHAIN_FILE=/home/andrey/Android/Sdk/ndk-bundle/build/cmake/android.toolchain.cmake \
      -DANDROID_NATIVE_API_LEVEL=${API_LEVEL} \
      -DBUILD_SHARED_LIBS=${BUILD_SHARED_LIB} \
      -GNinja ../boringssl
      
libssh cmake:

cmake \
	-DCMAKE_INSTALL_PREFIX=/opt/libssh-android \
	-DWITH_INTERNAL_DOC=OFF \
	-DWITH_GSSAPI=OFF \
	-DWITH_NACL=OFF \
	-DWITH_EXAMPLES=OFF \
	-DCMAKE_BUILD_TYPE=Release \
	-DCMAKE_TOOLCHAIN_FILE=${NDK_TOOLCHAIN_PATH} \
	-DANDROID_NDK="$ANDROID_NDK_ROOT" \
	-DANDROID_NATIVE_API_LEVEL=android-${API_LEVEL} \
	-DANDROID_ABI=${ANDROID_API} \
	-DBUILD_STATIC_LIB=${build_static_libssh} \
	-DBUILT_LIBS_DIR=${OUTPUT_LIBS_DIR} \
	-DWITH_ZLIB=1 \
	-DWITH_SERVER=1 \
	-DWITH_SFTP=1 \
	..
