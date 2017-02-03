# Custom time picker
An example that shows how to fix the problem of scrolling a time/date picker when is inside of a Scrollview.

#Motivation
Some time ago I was building an app that contains a timepicker inside of a Scrollview (wrappered by a LinearLayout) and I realized that there was a problem scrolling the time picker to select a time value. Yes, the Scrollview was the "owner of the touches". Of course, this is a problem that occurs since a long time. So, the solution is to create a custom time/date picker to override one of his method. In my example, I worked with a time picker but is valid for date piker too.
<br/>
<br/>
#Getting started
Open Android Studio, create a **new project** and choose an **empty Activity**. Now, create a **new java class** and extend it from **TimePicker**, see the [CustomTimePicker.java](https://github.com/betianaminio/android-custom-time-picker/blob/master/app/src/main/java/com/betianaminio/customtimepicker/CustomTimePicker.java) file. You need to provide three constructors to call the base builders, see [here](https://developer.android.com/reference/android/widget/TimePicker.html) for more information. After that comes the most important, override the **onInterceptTouchEvent** method with the following:
<br/>

    @Override
    public boolean onInterceptTouchEvent(MotionEvent motionEvent){

        if ( motionEvent.getActionMasked() == MotionEvent.ACTION_DOWN){

            ViewParent viewParent = getParent();

            if ( viewParent != null )
                viewParent.requestDisallowInterceptTouchEvent(true);
        }

        return false;
    }

Finally, in the activity's layout, add the custom time picker as:

            <com.betianaminio.customtimepicker.CustomTimePicker
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="30dp"
                android:id="@+id/custom_time_picker"/>
                
You have to use your own package ;).

If you need to access to your custom time picker from java code, works as a normal android visual component:

    CustomTimePicker myTimePicker = (CustomTimePicker)findViewById(R.id.custom_time_picker)
