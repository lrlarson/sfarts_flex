package {
    import com.adobe.viewsource.ViewSource;
    import com.yahoo.maps.api.YahooMap;
    import com.yahoo.maps.api.YahooMapEvent;
    import com.yahoo.maps.api.core.location.LatLon;
    import com.yahoo.maps.api.markers.SearchMarker;
    import com.yahoo.maps.webservices.local.LocalSearch;
    import com.yahoo.maps.webservices.local.LocalSearchItem;
    import com.yahoo.maps.webservices.local.LocalSearchResults;
    import com.yahoo.maps.webservices.local.events.LocalSearchEvent;
    
    import flash.display.Sprite;

    public class YahooMap_LocalSearch extends Sprite
    {
        private var _yahooMap:YahooMap;
        private var _localSearch:LocalSearch;
        
        public function YahooMap_LocalSearch()
        {
            ViewSource.addMenuItem(this, "srcview/index.html", true);
            
            this.stage.align = "topLeft";
            this.stage.scaleMode = "noScale";
            
            // this examples uses an application id passed into the app via FlashVars.
            // Get your own from the Yahoo! Developer Network @ http://developer.yahoo.com/wsregapp/
            var appid:String = this.loaderInfo.parameters.appid;
            
            _yahooMap = new YahooMap();
            _yahooMap.addEventListener(YahooMapEvent.MAP_INITIALIZE, handleMapInitialize, false, 0, true);
            _yahooMap.init(appid, this.stage.stageWidth, this.stage.stageHeight);
            
            _yahooMap.addPanControl(); // adds ability to pan and click on the map.
            _yahooMap.addZoomWidget(); // adds a zoom control widget to the map.
            _yahooMap.addTypeWidget(); // adds a map type control widget to the map.
            
            this.addChild(_yahooMap); // adds the yahoomap object to the display list.
        }
        
        private function handleMapInitialize(event:YahooMapEvent):void {
            _yahooMap.zoomLevel = 5; // sets the zoom level to a high-level city view.
            _yahooMap.centerLatLon = new LatLon(37.779160,-122.420049); // setting the center latlon over san francisco,ca
            
            _localSearch = new LocalSearch();
            _localSearch.addEventListener(LocalSearchEvent.SEARCH_SUCCESS, handleSearchSuccess);
            _localSearch.searchLocal("Pizza", _yahooMap.zoomLevel, _yahooMap.centerLatLon, 25, 1, 25, "96926236" ); // passing the 'Restaurants' ycatfilt id.
        }
        
        private function handleSearchSuccess(event:LocalSearchEvent):void {
            var searchResults:LocalSearchResults = event.data as LocalSearchResults;
            var results:Array = searchResults.results;
            var len:int = results.length;
            
            for(var i:int=0; i<len; i++) {
                var item:LocalSearchItem = results[i];
                var marker:SearchMarker = new SearchMarker(item);
                
                _yahooMap.markerManager.addMarker(marker);
                
            }
        }
    }
}
