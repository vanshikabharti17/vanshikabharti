# vanshikabharti
Q1
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class App {
    public static void main(String[] args) {
        sendPostRequest();
    }

    public static void sendPostRequest() {
        try {
            URL url = new URL("https://bfhldevapigw.healthrx.co.in/hiring/generateWebhook/JAVA");
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("POST");
            conn.setRequestProperty("Content-Type", "application/json");
            conn.setDoOutput(true);

            String jsonInput = """
                {
                  "name": "John Doe",
                  "regNo": "REG12347",
                  "email": "john@example.com"
                }
                """;

            try (OutputStream os = conn.getOutputStream()) {
                byte[] input = jsonInput.getBytes("utf-8");
                os.write(input, 0, input.length);
            }

            int responseCode = conn.getResponseCode();
            System.out.println("POST Response Code: " + responseCode);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}


Q2  import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class SubmitAnswer {
    public static void main(String[] args) {
        String webhookUrl = "https://example.com/webhook-url"; // Replace with actual webhook
        String accessToken = "your-jwt-token-here"; // Replace with actual token
        sendAnswer(webhookUrl, accessToken);
    }

    public static void sendAnswer(String webhookUrl, String accessToken) {
        try {
            URL url = new URL(webhookUrl);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("POST");
            conn.setRequestProperty("Content-Type", "application/json");
            conn.setRequestProperty("Authorization", "Bearer " + accessToken);
            conn.setDoOutput(true);

            String jsonAnswer = """
                {
                  "answer": "your-answer-here"
                }
                """;

            try (OutputStream os = conn.getOutputStream()) {
                byte[] input = jsonAnswer.getBytes("utf-8");
                os.write(input, 0, input.length);
            }

            int responseCode = conn.getResponseCode();
            System.out.println("Answer Submission Response Code: " + responseCode);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

Q3  SELECT 
    e1.EMP_ID,
    e1.FIRST_NAME,
    e1.LAST_NAME,
    d.DEPARTMENT_NAME,
    COUNT(e2.EMP_ID) AS YOUNGER_EMPLOYEES_COUNT
FROM 
    EMPLOYEE e1
JOIN 
    DEPARTMENT d ON e1.DEPARTMENT = d.DEPARTMENT_ID
LEFT JOIN 
    EMPLOYEE e2 ON e1.DEPARTMENT = e2.DEPARTMENT 
                AND e1.DOB < e2.DOB
GROUP BY 
    e1.EMP_ID, e1.FIRST_NAME, e1.LAST_NAME, d.DEPARTMENT_NAME
ORDER BY 
    e1.EMP_ID DESC;
