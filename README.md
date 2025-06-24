# URL-Shortener

import java.util.HashMap;
import java.util.Random;

public class URLShortener {
    private HashMap<String, String> urlMap;
    private String baseUrl;
    private String characters;
    private Random random;

    public URLShortener() {
        urlMap = new HashMap<>();
        baseUrl = "http://short.ly/";
        characters = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
        random = new Random();
    }

    // Method to generate a random 6-character short key
    private String generateShortKey() {
        StringBuilder key = new StringBuilder();
        for (int i = 0; i < 6; i++) {
            key.append(characters.charAt(random.nextInt(characters.length())));
        }
        return key.toString();
    }

    // Method to shorten the URL
    public String shortenURL(String originalURL) {
        String shortKey = generateShortKey();
        String shortURL = baseUrl + shortKey;
        urlMap.put(shortKey, originalURL);
        return shortURL;
    }

    // Method to retrieve the original URL
    public String retrieveURL(String shortURL) {
        String shortKey = shortURL.replace(baseUrl, "");
        return urlMap.get(shortKey);
    }

    public static void main(String[] args) {
        URLShortener shortener = new URLShortener();

        // Example usage
        String longURL = "https://www.example.com/some/very/long/url/path";
        String shortURL = shortener.shortenURL(longURL);

        System.out.println("Original URL: " + longURL);
        System.out.println("Shortened URL: " + shortURL);

        String retrievedURL = shortener.retrieveURL(shortURL);
        System.out.println("Retrieved URL: " + retrievedURL);
    }
}
