 RestTemplate restTemplate = new RestTemplate();

        HttpHeaders headers = new HttpHeaders();
        headers.setContentType(MediaType.APPLICATION_JSON);
        headers.set("Authorization", "key=" + SERVER_KEY);

        JSONObject body = new JSONObject();
        body.put("to", "YOUR_DEVICE_TOKEN");

        JSONObject notification = new JSONObject();
        notification.put("title", "Test Title");
        notification.put("body", "Test Body");

        body.put("notification", notification);

        HttpEntity<String> request = new HttpEntity<>(body.toString(), headers);

        ResponseEntity<String> response = restTemplate.exchange(FCM_URL, HttpMethod.POST, request, String.class);

        System.out.println("Response: " + response.getBody());
