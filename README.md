# deepseek
#docker-compose
version: '3.8'

services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama_container
    ports:
      - "11434:11434"
    volumes:
      - ollama_data:/root/.ollama
    restart: unless-stopped

volumes:
  ollama_data:




  ..................................................



  import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;
import org.apache.commons.csv.*;
import java.io.*;
import java.util.*;

@RestController
@RequestMapping("/api/csv")
public class CsvController {

    @PostMapping("/extract-emails")
    public ResponseEntity<Map<String, Object>> extractEmails(@RequestParam("file") MultipartFile file) {
        Map<String, Object> response = new HashMap<>();
        
        if (file.isEmpty()) {
            response.put("error", "File is empty");
            return ResponseEntity.badRequest().body(response);
        }
        
        if (!file.getOriginalFilename().endsWith(".csv")) {
            response.put("error", "File must be a CSV");
            return ResponseEntity.badRequest().body(response);
        }
        
        try (Reader reader = new BufferedReader(new InputStreamReader(file.getInputStream()))) {
            CSVParser csvParser = new CSVParser(reader, CSVFormat.DEFAULT.withFirstRecordAsHeader());
            List<String> emails = new ArrayList<>();
            
            for (CSVRecord record : csvParser) {
                String email = record.get("email"); // assumes column named "email"
                if (email != null && !email.trim().isEmpty()) {
                    emails.add(email.trim());
                }
            }
            
            response.put("emails", emails);
            response.put("count", emails.size());
            return ResponseEntity.ok(response);
            
        } catch (IOException e) {
            response.put("error", "Error processing CSV file: " + e.getMessage());
            return ResponseEntity.internalServerError().body(response);
        } catch (IllegalArgumentException e) {
            response.put("error", "CSV file doesn't contain 'email' column");
            return ResponseEntity.badRequest().body(response);
        }
    }
}
............................................

  
  # File upload settings
spring.servlet.multipart.max-file-size=10MB
spring.servlet.multipart.max-request-size=10MB

<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-csv</artifactId>
    <version>1.9.0</version>
</dependency>

....................

