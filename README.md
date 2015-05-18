HeaderRecyclerView
==================

HeaderRecyclerView is an Android library created to be able to use ``RecyclerView.Adapter`` with a header in a easy way. To use this library create your ``RecyclerView.Adapter`` classes extending from ``HeaderRecyclerViewAdapter``.

Screenshots
-----------

![Demo Screenshot][1]

Usage
-----

To use ``HeaderRecyclerView`` in your application you have to follow this steps:

* 1 - Create a class extending from ``HeaderRecyclerViewAdapter``:

```java

public class DragonBallAdapter extends HeaderRecyclerViewAdapter<RecyclerView.ViewHolder, DragonBallHeader, DragonBallCharacter> {


```

* 2 - Implement ``onCreateViewHolder`` and ``onBindViewHolder`` to create your ``RecyclerView.ViewHolder`` instances and draw your rows:

```java

@Override public RecyclerView.ViewHolder onCreateViewHolder(ViewGroup viewGroup, int viewType) {
    RecyclerView.ViewHolder viewHolder;
    LayoutInflater inflater = LayoutInflater.from(viewGroup.getContext());
    if (isHeaderType(viewType)) {
      View headerView = inflater.inflate(R.layout.row_dragon_ball_header, viewGroup, false);
      viewHolder = new HeaderViewHolder(headerView);
    } else {
      View characterView = inflater.inflate(R.layout.row_dragon_ball_character, viewGroup, false);
      viewHolder = new CharacterViewHolder(characterView);
    }
    return viewHolder;
  }

  @Override public void onBindViewHolder(RecyclerView.ViewHolder viewHolder, int position) {
    if (isHeaderPosition(position)) {
      DragonBallHeader header = getHeader();
      HeaderViewHolder headerViewHolder = (HeaderViewHolder) viewHolder;
      headerViewHolder.render(header);
    } else {
      DragonBallCharacter character = getItem(position);
      CharacterViewHolder characterViewHolder = (CharacterViewHolder) viewHolder;
      characterViewHolder.render(character);
    }
  }

```

* 3 - Configure your ``RecyclerView`` widget with this layout:

```java

  List<DragonBallCharacter> characters = getDragonBallCharacters();
  DragonBallHeader header = getHeader(characters);
  adapter.setHeader(header);
  adapter.setItems(characters);
  recyclerView.setAdapter(adapter);

```

**You can use methods like ``isHeaderType(viewType)`` or ``isHeaderPosition(position)`` to return the ViewHolder associated to the header or to draw the view associated to the header. The header instance can be obtained using the method ``getHeader()``**.

* 4 - If you are using a ``GridLayoutManager`` instead of a ``LinearLayoutManager`` remember you'll have to configure the ``SpanSizeLookup`` used in the ``LayoutManager`` instance. If you are using ``HeaderRecyclerView`` with a ``GridLayoutManager`` you can create an instance of ``HeaderSpanSizeLookup`` and configure your ``LayoutManager`` instance:

```java

  GridLayoutManager layoutManager = new GridLayoutManager(this, NUMBER_OF_COLUMNS);
  HeaderSpanSizeLookup headerSpanSizeLookup = new HeaderSpanSizeLookup(adapter, layoutManager);
  layoutManager.setSpanSizeLookup(headerSpanSizeLookup);

```

Add it to your project
----------------------

Add ``HeaderRecyclerView`` dependency to your ``build.gradle`` file

```groovy

dependencies{
    compile 'com.karumi:headerrecyclerview:1.0.0'
}

```

or to your ``pom.xml`` if you are using Maven instead of Gradle

```xml

<dependency>
    <groupId>com.karumi</groupId>
    <artifactId>headerrecyclerview</artifactId>
    <version>1.0.0</version>
    <type>aar</type>
</dependency>

```

Do you want to contribute?
--------------------------

Please, do it! We'd like to improve this library with your help :)

Libraries used in this project
------------------------------

* [Robolectric] [2]
* [JUnit] [3]
* [Picasso] [4]
* [Nox] [5]

License
-------

    Copyright 2015 Karumi

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.


[1]: ./art/screenshot_demo_1.gif
[2]: https://github.com/robolectric/robolectric
[3]: https://github.com/junit-team/junit
[4]: https://github.com/square/picasso
[5]: https://github.com/pedrovgs/Nox
