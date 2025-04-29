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




.............................
................................



# Step 1: Add upstream remote if not already added
git remote add upstream https://github.com/ORIGINAL_REPO_OWNER/REPO_NAME.git

# Step 2: Fetch the latest from upstream
git fetch upstream

# Step 3: Checkout your problematic branch
git checkout release/25.1_features

# Step 4: Hard reset to upstream's version of this branch (or main if it doesn't exist)
git reset --hard upstream/main  # or upstream/release/25.1_features if exists

# Step 5: Force push to your fork
git push origin release/25.1_features --force

