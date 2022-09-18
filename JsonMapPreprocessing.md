# Json 파일을 Map으로 전처리하기


```
Map<String, List<JsonObject>> map = new HashMap<>();
		// map 전처리
		for (Object object : item) {
			JsonObject objCate = (JsonObject) object;
			String key = objCate.get("category").getAsString();
			if (key.equals("REH") || key.equals("TMP")) {
				if (map.containsKey(key)) {
					List<JsonObject> list = map.get(key);
					list.add(objCate);
				} else {
					List<JsonObject> jsonlist = new ArrayList<>();
					jsonlist.add(objCate);
					map.put(key, jsonlist);
				}
			}
			//System.out.println("map : " + map.toString());
		}
		
		Iterator<Map.Entry<String, List<JsonObject>>> entries = map.entrySet().iterator();
		while(entries.hasNext()) {
			Map.Entry<String, List<JsonObject>> entry = entries.next();
			System.out.println("Key : "+ entry.getKey() + " , Value = " + entry.getValue());
		}
		
		List<MyWeatherDTO> list = new ArrayList<>();

		List<JsonObject> rehList = map.get("REH");
		List<JsonObject> tmpList = map.get("TMP");
		for (JsonObject tmp : tmpList) {
			for (JsonObject reh : rehList) {
				String fcstDate = reh.get("fcstDate").getAsString();
				String fcstTime = reh.get("fcstTime").getAsString().substring(0,2);
				String rehVal = reh.get("fcstValue").getAsString();
				if (fcstDate.equals(tmp.get("fcstDate").getAsString()) || fcstTime.equals(tmp.get("fcstTime").getAsString())) {
					String bDate = tmp.get("baseDate").getAsString();
					String bTime = tmp.get("baseTime").getAsString().substring(0,2);
					String tmpVal = tmp.get("fcstValue").getAsString();
					MyWeatherDTO dto = new MyWeatherDTO(bDate, bTime, fcstDate, fcstTime, rehVal, tmpVal);
					//System.out.println(dto.toString());
					list.add(dto);
				}
			}
		}
```