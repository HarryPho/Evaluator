package assignment3;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;
import java.util.stream.Stream;

@SuppressWarnings("unchecked")
public class Evaluator {

    public HashMap<String, Object> evaluate(String SSN, String firstName, String lastName, Function<String, Map<String, String>>... backgroundChecks) {

        if (backgroundChecks.length == 0)
            throw new RuntimeException("No background check service provided");

        List<String> reasonList = new ArrayList<>();

        HashMap<String, Object> results = new HashMap<>();
        results.put("SSN", SSN);
        results.put("firstName", firstName);
        results.put("lastName", lastName);
        results.put("reason", reasonList);

        Stream.of(backgroundChecks).map(criteria -> {
            Map<String, String> currentChecker = criteria.apply(SSN);
            reasonList.add(currentChecker.get("reason"));

            if (currentChecker.get("checkStatus") == "Rejected" && results.get("checkStatus") == null)
                results.put("checkStatus", "Rejected");

            return results;

        }).collect(Collectors.toList());

        if (results.get("checkStatus") == null)
            results.put("checkStatus", "Approved");

        return results;
    }
}