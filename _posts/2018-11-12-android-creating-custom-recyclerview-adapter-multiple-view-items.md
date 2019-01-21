---
ID: 462
post_title: >
  Creating custom RecyclerView adapter
  with multiple view items example
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/android-creating-custom-recyclerview-adapter-multiple-view-items/
published: true
post_date: 2018-11-12 15:57:49
---
<b>RecyclerView</b> has been the defacto for viewing lists in android. The solid performance and the ability to plugin any feature into a list without breaking a sweat made it the developer favorite. Ultimately replacing Listviews from being the standard way of displaying lists in android applications. What makes the RecyclerView the go-to library when thinking about lists?

For years the way developers used to think about viewing lists was quite straightforward. Having a linear set of views and simply populating it with the data, sounds like the jobs done! But things get really messy when this size of the list grows and effs up the user experience of the app by dropping frames and sloppy scroll behavior. RecyclerView was introduced with this magical formula of reusing the views without compromising the performance and memory. It made animations easy to implement on these lists for the addition or removal of items, made it damn easy to build lists that supported grids, horizontal or vertical scrolling or event scrolling the entire thing upside down (pssst... chats)!

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="2974167105"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>
<h2>How does a RecyclerView work?</h2>
Having a deeper understanding of the RecyclerView and the RecyclerViewAdapter will help a lot in writing efficient code. Let's see what makes RecyclerView awesome. At the core, the view is known for it's recycling ability of child views that help reduce memory usage (That's where the name comes from). At first, RecyclerView initializes a set of child views to display a certain amount of contents in the list to fill the viewport of the screen. Once the user starts scrolling, the view which gets past the screen boundary is used to repopulate and reused at the other end, this is done by the Adapter.

Let's take an example. Consider a RecyclerView displaying a list of contacts, where each contact is displayed as a card. If the screen has the size to fit 5 such contact cards, recycler view keeps a lower bound of a few extra cards and initializes it to give a smooth scrolling effect. So, if the RecyclerView has created a set of 7 views ready to display despite even if the data is way larger than that, and the viewport can fit 5, once the user starts scrolling, the 6th, and 7th come into the display while the views 1 and 2 exits the screen. These views 1 and 2 are then used to repopulate with the data and added back to the list's bottom making it enter as the 8th and 9th card in the view.
<h2>Creating a Custom RecyclerView Adapter</h2>
Before attaching a Custom Adapter to the RecyclerView, make sure you have included the RecyclerView view tags in the layout (xml) file.
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;RecyclerView
    android:id="@+id/recycler_view"
    android:scrollbars="vertical"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"/&gt;</pre>
And, We need one more layout file which will be used as the view for each row or item in the <code>RecyclerView</code>, Simply to use as a template. We'll take an example of a simple contact list. Create a new XML layout file in <code>res/layout/</code> with your desired layout design.
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/main_parent"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="5dp"&gt;
    &lt;TextView
        android:id="@+id/txt_name"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="18sp"
        android:padding="5dp"/&gt;
    &lt;TextView
        android:id="@+id/txt_number"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="15sp"
        android:padding="5dp"/&gt;
&lt;/LinearLayout&gt;</pre>
We need to create a POJO class (Plain Old Java Object) to represent each data item as an object while passing it down to the adapter, without dropping a sweat, android studio helps to add all the necessary getters, setters and constructors into the class through shortcuts (ALT + INSERT) after giving the basic details. Create a Java Class to hold the necessary information regarding the data objects.
<pre class="EnlighterJSRAW" data-enlighter-language="java">public class Contact {

    private String name;
    private String number;

    public Contact(String name, String number) {
        this.name = name;
        this.number = number;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getNumber() {
        return number;
    }

    public void setNumber(String number) {
        this.number = number;
    }
}
</pre>
Now Let's start working on the custom Adapter for the RecyclerView. Create a new Java Class extending the <code>RecyclerView.Adapter</code> and override the following methods from the parent class. We also need to create a nested sub-class extending the <code>RecyclerView.ViewHolder</code> which helps to create ViewHolders which populates data to the views present in the recyclerView. Once we wire up everything, our Custom adapter will look something similar to this.
<pre class="EnlighterJSRAW" data-enlighter-language="java">public class MyAdapter extends RecyclerView.Adapter&lt;MyAdapter.ContactHolder&gt; {

    // List to store all the contact details
    private ArrayList&lt;Contact&gt; contactsList;
    private Context mContext;

    // Counstructor for the Class
    public VideoListAdapter(ArrayList&lt;Contact&gt; contactsList, Context context) {
        this.contactsList = contactsList;
        this.mContext = context;
    }

    // This method creates views for the RecyclerView by inflating the layout
    // Into the viewHolders which helps to display the items in the RecyclerView
    @Override
    public ContactHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        LayoutInflater layoutInflater = LayoutInflater.from(parent.getContext());

        // Inflate the layout view you have created for the list rows here
        View view = layoutInflater.inflate(R.layout.contact_list_item, parent, false);
        return new ContactHolder(view);
    }

    @Override
    public int getItemCount() {
        return contactList == null? 0: contactList.size();
    }

    // This method is called when binding the data to the views being created in RecyclerView
    @Override
    public void onBindViewHolder(@NonNull ContactHolder holder, final int position) {
        final Contact contact = contactList.get(position);
        
        // Set the data to the views here
        holder.setContactName(contact.getName());
        holder.setContactNumber(contact.getNumber());

       // You can set click listners to indvidual items in the viewholder here
       // make sure you pass down the listner or make the Data members of the viewHolder public
    
    }

    // This is your ViewHolder class that helps to populate data to the view
    public class ContactHolder extends RecyclerView.ViewHolder {

        private TextView txtName;
        private TextView txtNumber;
        
        public ContactHolder(View itemView) {
            super(itemView);

            txtName = itemView.findViewById(R.id.txt_name);
            txtNumber = itemView.findViewById(R.id.txt_number);
        }
 
        public void setContactName(String name) {
            txtName.setText(name);
        }

        public void setContactNumber(String number) {
            txtNumber.setText(number);
        }
    }
}</pre>
&nbsp;

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="2974167105"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

<h3>Rigging up everything together in the Activity</h3>
It's time we connect all the dots together and have our RecyclerView go up and running in the activity. Head back to the Activity Class and add the following things to set it up. We need an instance of RecyclerView and the Custom Adapter we just created, plus a list to hold all the contact details. You can either hardcode the values of the contact or asynchronously load the data into the list and pass it down to the adapter to do the job of displaying it in the RecyclerView.
<pre class="EnlighterJSRAW" data-enlighter-language="java">public class MainActivity extends AppCompatActivity {

    private MyAdapter listAdapter;
    private ArrayList&lt;Contact&gt; contactsList = new ArrayList&lt;&gt;();
    private RecyclerView recycler;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        recycler = findViewById(R.id.recycler_view);
        LinearLayoutManager layoutManager = new LinearLayoutManager(this);
        recycler.setLayoutManager(layoutManager);
        listAdapter = new MyAdapter(contactsList, this);
        recycler.setAdapter(listAdapter);
        
        //Load the date from the network or other resources
        //into the array list asynchronously 
        
        contactsList.add(new Contact("Daniel Shiffman", "778899009"));
        contactsList.add(new Contact("Jhon Doe", "778899009"));
        contactsList.add(new Contact("Jane Doe", "778899009"));
        
        listAdapter.notifyDataSetChanged();
    }
}
</pre>
&nbsp;
<h2>Creating Custom Recycler Adapter for Multiple Views</h2>
This is an often misunderstood concept which has a verity of different implementation to get the job done. For a better performance of the RecyclerView we have to create an adapter with Multiple ViewHolder classes. Often seen way is to use visibility to control the views inside a single view holder, which is vaguely wrong way of doing this. Let's have a look at a RecyclerView Adapter which implements multiple views.
What we need:
<ul>
 	<li>Multiple Layout template files for items</li>
 	<li>POJO classeswith type indicator variables if the data is hetrogenous</li>
 	<li>Multiple ViewHolders inside the Adapter</li>
</ul>
Rest all the implementation of the custom adapter is same as the previous one, except the Multiple view adapter's class and the POJO will look similar to the following.
<pre class="EnlighterJSRAW" data-enlighter-language="java">public class Contact {

    //Add the type indicators here
    public static final int TEXT_TYPE = 0;
    public static final int IMAGE_TYPE = 0;

    private int viewType;
    private String name;
    private String number;

    public Contact(int viewType,String name, String number) {
        this.viewType = viewType;
        this.name = name;
        this.number = number;
    }
    
    public int getViewType() {
       return viewType;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getNumber() {
        return number;
    }

    public void setNumber(String number) {
        this.number = number;
    }
}
</pre>
Note that we are using a unique integer to note the type of view the object requires in the RecyclerView. This indicator can be used in the RecyclerView Adapter to use a specific layout with the ViewHolder. Here the Notable parts are the ViewType indicator variables in the data class (model class), the overding of &lt;code&gt;getItemViewType()&lt;/code&gt; method and switching the layouts based on this on the onCreateViewHoder method.
<pre class="EnlighterJSRAW" data-enlighter-language="java">public class MyAdapter extends RecyclerView.Adapter&lt;RecylerView.ViewHolder&gt; {

    // List to store all the contact details
    private ArrayList&lt;Contact&gt; contactsList;
    private Context mContext;

    // Counstructor for the Class
    public VideoListAdapter(ArrayList&lt;Contact&gt; contactsList, Context context) {
        this.contactsList = contactsList;
        this.mContext = context;
    }

    // This method creates views for the RecyclerView by inflating the layout
    // Into the viewHolders which helps to display the items in the RecyclerView
    @Override
    public RecyclerView.ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        LayoutInflater layoutInflater = LayoutInflater.from(parent.getContext());

        // Inflate the layout view you have created for the list rows here
        // use the viewType to inflate specic Layouts for the ViewHolders
        
        switch(viewType) {
             case Contact.TEXT_TYPE:
                   // Inflate the first view type
                   View view = layoutInflater.inflate(R.layout.list_layout_1, parent, false);
                   return new ViewHolder1(view);
             case Contact.TEXT_TYPE:
                   // inflate the second view type
                   View view = layoutInflater.inflate(R.layout.list_layout_2, parent, false);
                   return new ViewHolder2(view);
        }
        // always use a fallback ViewHolder
        View view = layoutInflater.inflate(R.layout.default_list_layout, parent, false);
        return new ViewHolder(view);
    }

    @Override
    public int getItemCount() {
        return contactList == null? 0: contactList.size();
    }

    @Override
    public int getItemViewType(int position) {
        int type = contactsList.get(position).getViewType();
        return type;
    }

    // This method is called when binding the data to the views being created in RecyclerView
    @Override
    public void onBindViewHolder(@NonNull ContactHolder holder, final int position) {
        final Contact contact = contactList.get(position);
        
        // Set the data to the views here
        holder.setContactName(contact.getName());
        holder.setContactNumber(contact.getNumber());

       // You can set click listners to indvidual items in the viewholder here
       // make sure you pass down the listner or make the Data members of the viewHolder public
    
    }

    // This is your ViewHolder class that helps to populate data to the view
    public class viewHolder1 extends RecyclerView.ViewHolder {
       // Your First view holder
       // Connect with the items in the layout here
    }
   
   public class viewHolder2 extends RecyclerView.ViewHolder {
       // Your Second view holder
       // Connect with the items in the layout here
    }
}</pre>
&nbsp;

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle" style="display: block; text-align: center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-7556700931518738" data-ad-slot="2974167105"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>