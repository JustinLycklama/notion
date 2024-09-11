# Apple APIs

# ScreenTime API

## Family controls

Authorizations

- Stops family controls app from being removed
- provides API into screen time via app tokens

## Managed Settings

Restrictions

- Filter web traffic
- shield activity

Managed Setting stores automatically shared between app + extensions

## Device Activity Center

Usage monitoring

- Execute code on timing windows when something has exceeded threshold.

Time monitoring using a Device Activity Extension

---

# Healthkit API

Will not be using for ScreenTimeHero, does not give the data I want

- **`HKStatisticsQuery`**
    
    
    Per ChatGPT:
    
    The **`HKStatisticsQuery`** class in the HealthKit framework allows you to query aggregated statistics for a specific health data type over a specified time range. While HealthKit doesn't provide direct access to detailed screen time data, you can use **`HKStatisticsQuery`** to retrieve aggregate metrics related to device usage patterns, such as pickups, pickups per hour, and screen time.
    
    ```jsx
    import HealthKit
    
    // Create an instance of HKHealthStore
    let healthStore = HKHealthStore()
    
    // Define the data type you want to query (e.g., device usage data)
    let dataType = HKObjectType.categoryType(forIdentifier: .appleStandHour)
    
    // Define the date interval for the query (e.g., today)
    let startDate = Calendar.current.startOfDay(for: Date())
    let endDate = Date()
    
    // Create an HKStatisticsQuery instance
    let query = HKStatisticsQuery(quantityType: dataType!, quantitySamplePredicate: nil, options: .cumulativeSum, anchorDate: startDate, intervalComponents: DateComponents(day: 1)) { (query, result, error) in
        guard let result = result else {
            print("Error fetching statistics: \(String(describing: error))")
            return
        }
        
        // Process the query results
        if let sum = result.sumQuantity() {
            let value = sum.doubleValue(for: HKUnit.count())
            print("Aggregate usage data: \(value)")
        } else {
            print("No data available")
        }
    }
    
    // Execute the query
    healthStore.execute(query)
    ```