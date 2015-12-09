# jenkins
jekins config
Since jenkins does no support the pachage of ipa , so a script is needed to do this


if [ -d "${WORKSPACE}/build" ]; then rm -rf ${WORKSPACE}/build; fi;
mkdir ${WORKSPACE}/build;
if [ -d "${WORKSPACE}/build/${BUILD_NUMBER}" ]; then rm -rf ${WORKSPACE}/build/${BUILD_NUMBER}; fi;
mkdir -p ${WORKSPACE}/build/${BUILD_NUMBER};
xcodebuild -project ${WORKSPACE}/flyertea-app-ios-cibuild/FeiKe/FKForum.xcodeproj -scheme "FKForum" -sdk iphoneos archive -archivePath ${WORKSPACE}/build/${BUILD_NUMBER}/archive CODE_SIGN_IDENTITY="iPhone Developer: Mingshan Zheng (T4E8LVDEY2)"
xcodebuild -exportArchive -exportFormat IPA -archivePath ${WORKSPACE}/build/${BUILD_NUMBER}/archive.xcarchive -exportPath ${WORKSPACE}/build/${BUILD_NUMBER}/Flyertea-${VERSION}-${BUILD_DATE}-${BUILD_ID}.ipa -exportProvisioningProfile "d25593dc-1c99-4d51-8616-690b5805b116"
