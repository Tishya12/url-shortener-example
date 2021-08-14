# URL Shortener Example using Spring Boot & Redis

This example shows a simple URL Shortener implementation using
- Spring Boot 2.1.0 (Spring Web[MVC] + Spring Data Redis)
- Guava 18.0
- Common Validator 1.6

### URLs
- POST `/rest/url` with body as `long_url_string` - For creating the short url from long url
- GET `/rest/url/{id}` - For retrieving the long URL from short `id`

### java code for it
package urlShortner;
import java.util.HashMap;
import java.util.Random;
import java.lang.StringBuilder;
public class UrlShort {


        //HashMap to store the longUrl and the randomly generated string
        HashMap<String,String> urlMap = new HashMap<>();

        // Encodes a URL to a shortened URL.
        public String encode(String longUrl) {
            Random rand = new Random();
            int urlLen = 6;
            char [] shortURL = new char[urlLen];
            String randChars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234567890";

            for(int i = 0; i < urlLen; i++ )
                shortURL[i] = randChars.charAt(rand.nextInt(randChars.length()));

            StringBuilder sb = new StringBuilder("http://tinyurl.com/");
            sb.append(new String(shortURL));
            System.out.println(sb);

            urlMap.put(sb.toString(),longUrl);

            return sb.toString();

        }

        // Decodes a shortened URL to its original URL.
        public String decode(String shortUrl) {

            return urlMap.get(shortUrl);

        }

    public static void main(String args[]) {

 UrlShort codec = new UrlShort();
String url="https://www.interviewcake.com/question/java/url-shortener";
 String longurl=codec.decode(codec.encode(url));
 System.out.println(longurl);
}
}
