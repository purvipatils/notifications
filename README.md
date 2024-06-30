//import org.json.JSONObject;

@GetMapping("/sendNotification")
	public void sendNotification() {

		RestTemplate restTemplate = new RestTemplate();

		HttpHeaders headers = new HttpHeaders();
		headers.setContentType(MediaType.APPLICATION_JSON);
		headers.set("Authorization", "key=" + SERVER_KEY);

		JSONObject body = new JSONObject();
		body.put("to", DEVICE_TOKEN);

		JSONObject notification = new JSONObject();
		notification.put("title", "Test Title");
		notification.put("body", "Test Body");

		body.put("notification", notification);

		HttpEntity<String> request = new HttpEntity<>(body.toString(), headers);

		try {
			ResponseEntity<String> response = restTemplate.exchange(FCM_URL, HttpMethod.POST, request, String.class);
			logger.info("FCM Response: {}", response.getBody());
		} catch (Exception e) {
			logger.error("Error sending FCM notification", e);
		}
	}


