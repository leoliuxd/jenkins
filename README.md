# jenkins
jekins config
Since jenkins does no support the pachage of ipa , so a script is needed to do this


if [ -d "${WORKSPACE}/build" ]; then rm -rf ${WORKSPACE}/build; fi;
mkdir ${WORKSPACE}/build;
if [ -d "${WORKSPACE}/build/${BUILD_NUMBER}" ]; then rm -rf ${WORKSPACE}/build/${BUILD_NUMBER}; fi;
mkdir -p ${WORKSPACE}/build/${BUILD_NUMBER};
App_Infoplist_Path="${WORKSPACE}/FeiKe/FKForum/Info.plist"
#get version
VERSION=$(/usr/libexec/PlistBuddy -c "print CFBundleShortVersionString" ${App_Infoplist_Path})
#get build
BUILDVERSION=$(/usr/libexec/PlistBuddy -c "print CFBundleVersion" ${App_Infoplist_Path})
#get displayName
DISPLAYNAME=$(/usr/libexec/PlistBuddy -c "print CFBundleDisplayName" ${App_Infoplist_Path})
#get build date

BUILD_DATE=`date "+%Y-%m-%d"`

xcodebuild -project ${WORKSPACE}/flyertea-app-ios-cibuild/FeiKe/FKForum.xcodeproj -scheme "FKForum" -sdk iphoneos archive -archivePath ${WORKSPACE}/build/${BUILD_NUMBER}/archive CODE_SIGN_IDENTITY="iPhone Developer: Mingshan Zheng (T4E8LVDEY2)"
xcodebuild PROVISIONING_PROFILE=d25593dc-1c99-4d51-8616-690b5805b116 -exportArchive -exportFormat IPA -archivePath ${WORKSPACE}/build/${BUILD_NUMBER}/archive.xcarchive -exportPath ${WORKSPACE}/build/${BUILD_NUMBER}/Flyertea-${VERSION}-${BUILD_DATE}-${BUILD_ID}.ipa 
