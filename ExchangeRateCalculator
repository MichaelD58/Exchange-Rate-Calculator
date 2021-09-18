import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.nio.charset.StandardCharsets;
import java.util.*;
import java.text.DecimalFormat;

public class ExchangeRateCalculator {
  /**
   * Iterate through each line of input.
   */
  public static void main(String[] args) throws IOException {
    InputStreamReader reader = new InputStreamReader(System.in, StandardCharsets.UTF_8);
    BufferedReader in = new BufferedReader(reader);
    String line;
    while ((line = in.readLine()) != null) {
      determineExchangeRate(line);
    }
  }
  
  /**
   * In this method the input is split to get the required information and putting it into the HashMap which will be used
   * to store the currency pairs. Once additional methods are called to get the inverse values as well as calculate new rates, the output
   * is dealt with.
   */
  private static void determineExchangeRate(String line) {
    String[] input = line.split("\\|");
    String desiredRate =  input[1];//The rate that is being asked for
    String[] ratesArray = input[0].split(";");//The currency pair information
    HashMap<String, Double> rates = new HashMap<String, Double>();
    DecimalFormat decimalFormat = new DecimalFormat("0.00");//Format for the output (2 decimal places)
    
    //HashMap is filled with curency pairs with the name acting as the key and the rate as the value
    for(int i = 0; i < ratesArray.length; i++){
      String[] temp = new String[1];
      temp = ratesArray[i].split(":");
      rates.put(temp[0], Double.parseDouble(temp[1]));
    }

    rates = getInverses(rates);//Method is called that produces the inverse values of currency pairs
    rates = calculateNewRates(rates);//Method is called that calculates new currency pairs based on exisiting currency pairs
    
    if(desiredRate.substring(0, 3).equals(desiredRate.substring(3, 6))){//Check to see if the desired rate is the same currency, twice
      System.out.println(desiredRate + ":1.00");//Output for a 1:1 rate
    }else if(rates.containsKey(desiredRate)){//Check to see if the desired rate is known
      System.out.println(desiredRate + ":" + decimalFormat.format(rates.get(desiredRate)));
    }else{
       System.out.println("Unable to determine rate for " + desiredRate);//Output if the desired rate is not known
    }
  }
  
  /**
   * In this method the inverse values are calculated. This is done by checking if an inverse value of a currency pair is not already
   * in the HashMap, and if not, the inverse is calculated and the new currency paitr is added to the HashMap.
   */
  private static HashMap<String, Double> getInverses(HashMap<String, Double> rates){
    HashMap<String,Double> temp = new HashMap<>();//Temp HashMap that is used to store the new inverse currency pairs
    
    for(Map.Entry<String, Double> set : rates.entrySet()){
      String newRateName = set.getKey().substring(3, 6) + set.getKey().substring(0, 3);//Inverse name is created
      if(!rates.containsKey(newRateName)){// Check to see if inverse currency pair already exists
        Double newRate = 1 / set.getValue();//Inverse rate is calculated
        temp.put(newRateName, newRate);//Inverse currency pair is added to the temp HashMap
      }
    }
    rates.putAll(temp);//All currency pairs in the temp HashMap are added to the standard currency pair HashMap
    
    return rates;//HashMap is returned
  }
  
  /**
   * In this method, new currency pairs are calculated from pre-existing currency pairs. For example, we can calculate EURGBP from EURUSD and USDGBP.
   * If new currency pairs are calculated, then the inverse methd and this method are called once more as a new currency pair(s) exists.
   */
  private static HashMap<String, Double> calculateNewRates(HashMap<String, Double> rates){
    HashMap<String,Double> temp = new HashMap<>();//Temp HashMap that is used to store the new calculated currency pairs
    Boolean runAgain = false;//Used to keep track if a new currency pair has been calculated
    
    for(Map.Entry<String, Double> set1 : rates.entrySet()){
      for(Map.Entry<String, Double> set2 : rates.entrySet()){
        //If two currencies are linked by another currency (XY, YZ, XZ - XZ are linked through Y)
        if(set1.getKey().substring(3, 6).equals(set2.getKey().substring(0, 3)) && !(set1.getKey().substring(0, 3).equals(set2.getKey().substring(3, 6)))){
          String newRateName = set1.getKey().substring(0, 3) + set2.getKey().substring(3, 6);//New currency pair name is created
          if(!rates.containsKey(newRateName)){//If the new currency pair doesn't already exist
            Double newRate = set1.getValue() * set2.getValue();//XY, YZ, XZ - XZ is calculated by multiplying XY and YZ as Y is the common factor
            temp.put(newRateName, newRate);//New calculated currency pair is added to the temp HashMap
            runAgain = true;//Since a new currency pair has been created, the boolean that tracks whether the two methods will be run again is set to true
          }
        }
      }
    }
    
    rates.putAll(temp);//All currency pairs in the temp HashMap are added to the standard currency pair HashMap
    
    //If the boolean is true, the methods are run again
    if(runAgain){
      rates = getInverses(rates);
      calculateNewRates(rates);
    }
    
    return rates;//HashMap is returned
  }
}
