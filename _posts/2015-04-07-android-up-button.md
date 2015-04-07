---
layout: post
title: Android up button working like back
comments: True
---

In order to accomplish this, we have to first enable the up button, and then override onOptionsItemSelected() method which is invoked when up button is pressed:

{% highlight java %}
public class Child extends ActionBarActivity {

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    getSupportActionBar().setDisplayHomeAsUpEnabled(true);
  }

   @Override
  public boolean onOptionsItemSelected(MenuItem item) {
    switch (item.getItemId()) {
      case android.R.id.home:
        // go back to the prev screen
        onBackPressed();

        return true;
      default:
        return super.onOptionsItemSelected(item);
    }
  }
{% endhighlight %}

Here is a real life example when this is useful:
{% highlight xml %}
<!--AndroidManifest.xml-->
<activity android:name=".ui.Parent1"/>
<activity android:name=".ui.Child"
          android:parentActivityName=".ui.Parent1">
<activity android:name=".ui.Parent2"/>
{% endhighlight %}

In this example, Child is started from both Parent1 and Parent2. Assuming that we want the following scenario:

- started Child from Parent1 - up should brings us back to Parent1
- started Child from Parent2 - up should brings us back to Parent2

If we used the default impementation, pressing back would always take us to Parent1 activity. But with this change, pressing the up button in Child will take us back to the activity from which it was started.