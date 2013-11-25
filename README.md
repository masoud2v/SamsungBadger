SamsungBadger
=============

Simple class that abstracts interfacing with Samsung's TWLauncher BadgeProvider

Simply add as a library project to use.

EXAMPLES
=============

**Add the following permissions to your application's AndroidManifest.xml**

    <uses-permission android:name="com.sec.android.provider.badge.permission.READ" />
    <uses-permission android:name="com.sec.android.provider.badge.permission.WRITE" />


**The column structure is as follows:**

    (integer) _id, (text) package, (text) class, (integer) badgecount, (blob) icon


**To return the Badge instance for your application:**

    Context context = getApplicationContext();
    Badge badge = Badge.getBadge(context);
    if (Badge.isBadgingSupported(context)) {
        Badge badge = Badge.getBadge(context);

        // This indicates there is no badge record for your app yet
        if (badge == null) {
            return;
        } else {
            Log.d("Badge", badge.toString());
        }
    }


**To badge your icon with "1":**

    Context context = getApplicationContext();
    if (Badge.isBadgingSupported(context)) {
        Badge badge = new Badge();
        badge.mPackage = context.getPackageName();
        badge.mClass = getClass().getName(); // This should point to Activity declared as android.intent.action.MAIN
        badge.mBadgeCount = 1;
        badge.save(context);
    }


**To clear badge count on your app's icon:**

    Context context = getApplicationContext();
    if (Badge.isBadgingSupported(context)) {
        Badge badge = Badge.getBadge(context);
        if (badge != null) {
            badge.mBadgeCount = 0;
            badge.update(context);
        } else {
            // Nothing to do as this means you don't have a badge record with the BadgeProvider
            // Thus you shouldn't even have a badge count on your icon
        }
    }

LICENSE
=============

    Copyright 2013 Daniel Ochoa
    
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    
    http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
