# NotePad
* NoteList中显示条目增加时间戳显示
* 添加笔记查询功能（根据标题查询）
* 实验截图：
* ![](https://github.com/Haseus/notepad/blob/master/photo/1.png )
![](https://github.com/Haseus/notepad/blob/master/photo/2.png )
![](https://github.com/Haseus/notepad/blob/master/photo/3.png )
![](https://github.com/Haseus/notepad/blob/master/photo/4.png )
![](https://github.com/Haseus/notepad/blob/master/photo/5.png )
![](https://github.com/Haseus/notepad/blob/master/photo/6.png )
* 实验代码:
* note_search_list.xml
    > <TextView</br>
      android:id="@+id/text1_time"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:textAppearance="?android:attr/textAppearanceSmall"
      android:paddingLeft="5dip"
      android:textColor="@color/colorBlack"/>
* NoteSearch
    > private static final String[] PROJECTION = new String[] {
         NotePad.Notes._ID, 
         NotePad.Notes.COLUMN_NAME_TITLE, 
         NotePad.Notes.COLUMN_NAME_CREATE_DATE,      
 };
    > String[] dataColumns = { NotePad.Notes.COLUMN_NAME_TITLE ,  NotePad.Notes.COLUMN_NAME_CREATE_DATE } ;
int[] viewIDs = { android.R.id.text1 , R.id.text1_time };
* note_search_list.xml
    > <?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  android:orientation="vertical" android:layout_width="match_parent"
  android:layout_height="match_parent">
  <SearchView
      android:id="@+id/search_view"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:iconifiedByDefault="false"
      android:queryHint="输入搜索内容..."
      android:layout_alignParentTop="true">
  </SearchView>
  <ListView
      android:id="@android:id/list"
      android:layout_width="match_parent"
      android:layout_height="wrap_content">
  </ListView>
</LinearLayout>
* NoteSearch
    > private static final String[] PROJECTION = new String[] {
          NotePad.Notes._ID, 
          NotePad.Notes.COLUMN_NAME_TITLE, 
          NotePad.Notes.COLUMN_NAME_CREATE_DATE, 
  };
    > public boolean onQueryTextChange(String newText) {
      String selection = NotePad.Notes.COLUMN_NAME_TITLE + " Like ? ";
      String[] selectionArgs = { "%"+newText+"%" };
      Cursor cursor = managedQuery(
              getIntent().getData(),            
              PROJECTION,                       
              selection,                        
              selectionArgs,                    
              NotePad.Notes.DEFAULT_SORT_ORDER  
      );
      String[] dataColumns = { NotePad.Notes.COLUMN_NAME_TITLE ,  NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE };
      int[] viewIDs = { android.R.id.text1 , R.id.text1_time };
      MyCursorAdapter adapter = new MyCursorAdapter(
              this,
              R.layout.noteslist_item,
              cursor,
              dataColumns,
              viewIDs
      );
      setListAdapter(adapter);
      return true;
  }
 


