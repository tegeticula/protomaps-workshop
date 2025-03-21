# protomaps-workshop
Companion repo for my Knight Center class


## I don't want the world, just a slice of it

### Tiles for a city or country

tktk





### How I made the isolated NYC map

[add screenshot]

Making an isolated area map is nice, but not necessary.

Here's how I did it:

Essentially following [these instructions](https://docs.protomaps.com/basemaps/build), with some minor tweaks.

#### Get a geojson file of your city

We need to boundary of the city in order to "slice" data with it (and ignore everything else). Like a cookie-cutter.

- Go to https://spelunker.whosonfirst.org/
- Use the search box at the top to find the city or region you want
- Click into the area until you see the map you like. Here's New York City, for example
[image]
- Right-click (or control-click for Macs) on `As GeoJSON (raw data)`
[image]
- Give it a name and save to your downloads file. _Use the same name for all the later steps instead of `yourplace`_
- You may need to rename it so the extension is `.geojson` like `yourplace.geojson`

#### Get raw map data from OpenStreetMap (OSM)

OK, we're going to use that boundary to take a slice of map data from OpenStreetMap.

- Using a text editor, open the `.geojson` file you downloaded
- Copy that to your clipboard, for pasting in a moment
- Go to https://slice.openstreetmap.us/#0.41/0/0
- Paste the geojson text into the box that reads "Paste bbox or GeoJSON:"
- Click "Load"
- Name it the same name you used above instead of `yourplace`
- Click "Generate Slice"
- After a while, a "Download" link will appear. Click that. You will save a file that's `yourplace.pbf`

#### Put it all together

Here, use the names you used above instead of `yourplace` for your `.geojson` and `.pbf` files:

- Start the `protomaps-workshop` Codespace. Can be yours or mine. [tk how]
- Click into the terminal window
- Type `sudo apt update`
- Type `sudo apt install maven`
- Type `git clone https://github.com/protomaps/basemaps`
- Change into the tiles directory by typing `cd basemaps/tiles`
- Type `mvn clean package`
- Make a new directory by typing `mkdir -p data/sources`
- Open the Downloads folder on your computer
- Drag the `yourplace.geojson` file from your computer's Downloads folder into the `tiles` directory on your Codespace
- Drag the `yourplace.pbf` file from your computer's Downloads folder into the `data/sources` file on your Codespace
- Type (or copy-paste): `java -jar target/protomaps-basemap-HEAD-with-deps.jar --clip=yourplace.geojson --area=yourplace --download`
- Eventually you should end up with a `yourplace.pmtiles` file in your `tiles` directory. That's your tile file!
- Save this to your local computer by right-clicking (or control-clicking for Macs) on the `yourplace.pmtiles` file and choose "Download." It's important to save this! The Codespace will disappear eventually and you'll have to repeat all of these steps if you don't.

