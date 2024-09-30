# Blockchain-carbon-accounting

pragma solidity = 0.6.0;

contract Registration {

    address public EPA;  // 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
    mapping(address => bool) public Airline_Company; //0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2
    mapping(address => bool) public IATA; //0x4B20993Bc481177ec7E8f571ceCaE8A9e22C02db
    mapping(address=> bool) public Utility_Provider; //0x78731D3Ca6b7E34aC0F824c42a7cC18A495cabaB
    mapping(address => bool) public Airport_Authority; // 0x617F2E2fD72FD9D5503197092aC168c91465E7f2
    mapping(address => bool) public Aviation_Fuel_Transporter; //0x17F6AD8Ef982297579C203069C1DbfFE4348c372
    mapping(address => bool) public Carbon_offset_provider; //0x5c6B0f7Bf3E7ce046039Bd8FABdfD3f9F5021678
    mapping(address => bool) public Passenger;  //0x03C6FcED478cBbC9a4FAB34eF9f40767739D1Ff7
      
    modifier onlyEPA {
        require(msg.sender == EPA, "Sender not authorized.");
        _;
    }   
    
    constructor() public{
        EPA = msg.sender;
    }
    
    function registerAirline_Company(address a) external onlyEPA {
        require(!Airline_Company[a], "AirlineIndustry exists already");
        Airline_Company[a] = true;
    }
    
    function registerAviation_Fuel_Transporter(address f) external onlyEPA {
        require(!Aviation_Fuel_Transporter[f], "Aviation_Fuel_Transporter exists already");
        Aviation_Fuel_Transporter[f] = true;
    }
    
    function registerIATA(address i) external onlyEPA {
        require(!IATA[i], "IATA exists already");
        IATA[i] = true;
    }

    function registerUtility_Provider(address p) external onlyEPA {
        require(!Utility_Provider[p], "Electricity_Producer exists already");
        Utility_Provider[p] = true;
    }
    
    function registerAirport_Authority(address u) external onlyEPA {
        require(!Airport_Authority[u], "Airport_Authority exists already");
        Airport_Authority[u] = true;
    }

    function registerCarbon_offset_provider(address o) external onlyEPA {
        require(!Carbon_offset_provider[o], "Carbon_offset_provider exists already");
        Carbon_offset_provider[o] = true;
    }

    function registerPassenger(address p) external onlyEPA {
        require(!Passenger[p], "Passenger exists already");
        Passenger[p] = true;
    }
    
    function isEPA(address e) public view returns(bool) {
        return (EPA == e);
    }
    
    function Airline_CompanyExists(address a) public view returns(bool) {
        return Airline_Company[a];
    }
    
    function IATAExists(address i) public view returns(bool) {
        return IATA[i];
    }
    
    function Utility_ProviderExists(address p) public view returns(bool) {
        return Utility_Provider[p];
    }

    function Airport_AuthorityExists(address u) public view returns(bool) {
        return Airport_Authority[u];
    }
    function Carbon_offset_providerExists(address o) public view returns(bool) {
        return Carbon_offset_provider[o];
    }

    function Aviation_Fuel_TransporterExists(address f) public view returns(bool) {
        return Aviation_Fuel_Transporter[f];
    }
    function PassengerExists(address p) public view returns(bool) {
        return Passenger[p];
    }
}

contract Scope1CarbonEmission{

    uint256 public fuel_Consumed_in_Kg;
    uint256 public totalWeight_in_Kg;
    uint256 public totalFuelBurn_in_Kg;
    uint256 public fuelBurnPerPassenger_in_Kg;
    uint256 public co2EmissionPerPassenger_in_kg;
    uint256 public totalCo2Emitted_in_kg;
    uint256 public emissionFactor;
    address payable public airlineCompany;
    uint256 public Total_Carbon_cost;
    uint256 public Carbon_cost_per_passeneger;
    uint256 public total_number_of_passenegers_economy_class;
    uint256 public total_number_of_passenegers_premium_economy_class;
    uint256 public total_number_of_passenegers_business_class;
    uint256 public total_number_of_passenegers_first_class;
    uint256 public total_number_of_passengers;
    uint256 public total_passenger_FuelBurn_in_Kg;
    uint256 public Fuel_Burn_per_Economy_Class_Pax_kg;
    uint256 public Fuel_Burn_per_business_Class_Pax_kg;
    uint256 public Fuel_Burn_per_first_Class_Pax_kg;
    uint256 public first_class_cabin_factor;
    uint256 public economy_class_cabin_factor;
    uint256 public pre_economy_class_cabin_factor;   
    uint256 public business_class_cabin_factor;
    uint256 public totalFuelBurn_in_Kg_;
    uint256 public totalCo2Emitted_in_kg_;
    uint256 public Carbon_cost_per_passeneger_Economy_class;
    uint256 public Carbon_cost_per_passeneger_Premium_Economy_class;
    uint256 public Carbon_cost_per_passeneger_business_class;
    uint256 public Carbon_cost_per_passeneger_first_class;
    uint256 public Denom;
    uint256 public Fuel_Burn_per_Economy_Class_Pax_kg_NM;
    uint256 public Fuel_Burn_per_Economy_Class_Pax_kg_D1;
    uint256 public Fuel_Burn_per_Pre_Economy_Class_Pax_kg_D2;
    uint256 public Fuel_Burn_per_Economy_Class_Pax_kg_D3;
    uint256 public Fuel_Burn_per_Economy_Class_Pax_kg_D4;
    uint256 public Fuel_Burn_per_Economy_Class_Pax_kg_DF;
    uint256 public Co2_emitted_per_passenger_Economy_class;
    uint256 public Co2_emitted_per_passenger_Economy_Class;
    uint256 public Fuel_Burn_per_Premium_Economy_Class_Pax_kg_NM;
    uint256 public Fuel_Burn_per_Premium_Economy_Class_Pax_kg;
    uint256 public Co2_emitted_per_passenger_Premium_Economy_class; 
    uint256 public Co2_emitted_per_passenger_Premium_Economy_Class; 
    uint256 public Fuel_Burn_per_Business_Class_Pax_kg_NM;
    uint256 public Fuel_Burn_per_Business_Class_Pax_kg;
    uint256 public Co2_emitted_per_passenger_Business_class;
    uint256 public Co2_emitted_per_passenger_Business_Class;
    uint256 public Fuel_Burn_per_First_Class_Pax_kg_NM;
    uint256 public Fuel_Burn_per_First_Class_Pax_kg;
    uint256 public Co2_emitted_per_passenger_First_class;
    uint256 public Co2_emitted_per_passenger_First_Class;
    bool public Penalty;
    Registration public registrationContract;
    

	event aircraftEmissionStandardsUpdated (string fuel_grade,string emission_factor,  string Economy_class_cabin_factor, string  Prem_economy_class_cabin_factor, 		string  Business_class_cabin_factor, string  First_class_cabin_factor);
	
	constructor(address registration) public {
	        registrationContract = Registration(registration);
	        
	        require(registrationContract.Airline_CompanyExists(msg.sender), "Sender not authorized");
	        airlineCompany = payable(msg.sender);
	    }
	
	    modifier onlyAirlineIndustry {
	        require(registrationContract.Airline_CompanyExists(msg.sender), "Sender not authorized");
	        _;
	    }
	
	    modifier onlyIATA {
	        require(registrationContract.IATAExists(msg.sender), "Sender not authorized");
	        _;
	    }
	
	function updateAircraftemissionStandards (string memory fuel_grade,
	                                            string memory emission_factor,
	                                            string memory Economy_class_cabin_factor, string memory Prem_economy_class_cabin_factor, 
	                                            string memory Business_class_cabin_factor, string memory First_class_cabin_factor) public onlyIATA {
	emit aircraftEmissionStandardsUpdated (fuel_grade, emission_factor,Economy_class_cabin_factor,  Prem_economy_class_cabin_factor,   Business_class_cabin_factor,  First_class_cabin_factor);
	
	}
	
	// Update Passenger information
	event PassengerDetailsUpdated (uint256  total_number_of_passenegers_Economy_class, uint256  total_number_of_passenegers_Premium_economy_class, uint256  total_number_of_passenegers_Business_class, uint256 total_number_of_passenegers_First_class, uint256 total_number_of_Passengers,  uint256 total_Passenger_Weight_in_KG, uint256 total_cargoWeight_in_Kg, uint256 totalWeight_in_KG );
	
	function updatePassengerDetails (uint256 total_number_of_passenegers_Economy_class,  uint256 total_number_of_passenegers_Premium_economy_class, uint256 total_number_of_passenegers_Business_class, uint256 total_number_of_passenegers_First_class, uint256 total_Passenger_Weight_in_KG, uint256 total_cargoWeight_in_Kg ) external onlyAirlineIndustry {
	
	uint256 total_number_of_Passengers = uint256 (total_number_of_passenegers_economy_class) +  uint256 (total_number_of_passenegers_premium_economy_class) +
	                                     uint256 (total_number_of_passenegers_business_class) + uint256 (total_number_of_passenegers_first_class);
	uint256 totalWeight_in_KG = (uint256 (total_Passenger_Weight_in_KG) + uint256 (total_cargoWeight_in_Kg));
	
	emit PassengerDetailsUpdated (total_number_of_passenegers_Economy_class, total_number_of_passenegers_Premium_economy_class, total_number_of_passenegers_Business_class, total_number_of_passenegers_First_class, total_number_of_Passengers, total_Passenger_Weight_in_KG, total_cargoWeight_in_Kg, totalWeight_in_KG);
	}
	
	// Update Fuel levels
	
	event FuelLevelsUpdated ( uint256 fuelBeginning_in_Kg, uint256  fuelEnding_in_Kg,  uint256 fuel_Consumed_in_Kg);
	
	function updateFuelLevels ( uint256 fuelBeginning_in_Kg, uint256 fuelEnding_in_Kg) external onlyAirlineIndustry {
		
	require(fuelBeginning_in_Kg >= fuelEnding_in_Kg, "Initial fuel should be greater than or equal to final fuel");
		
	fuel_Consumed_in_Kg = (fuelBeginning_in_Kg - fuelEnding_in_Kg);
	
	emit FuelLevelsUpdated (fuelBeginning_in_Kg, fuelEnding_in_Kg, fuel_Consumed_in_Kg);
	
	
	}
	
	// Calculate Scope 1 carbon emission
	
	event Scope1CarbonEmissionCalculated(uint256 fuel_Consumed_in_Kg, uint256 totalWeight_in_KG,uint256 total_passenger_FuelBurn_in_Kg,
	                 uint256 Fuel_Burn_per_Economy_Class_Pax_kg, uint256 Fuel_Burn_per_Premium_Economy_Class_Pax_kg,
	                 uint256 Fuel_Burn_per_Business_Class_Pax_kg, uint256 Fuel_Burn_per_First_Class_Pax_kg,
	                uint256 Co2_emitted_per_passenger_Economy_class, uint256 Co2_emitted_per_passenger_Premium_Economy_class,
	                uint256 Co2_emitted_per_passenger_Business_class, uint256 Co2_emitted_per_passenger_First_class,uint256 totalCo2Emitted_in_kg);
	
	 
	
	   
	    function calculateScope1CarbonEmission(
	        address receiver_EPA,
	        address receiver_IATA,
	        uint256 fuelBeginning_in_Kg,
	        uint256 fuelEnding_in_Kg,
	        uint256 total_Passenger_Weight_in_KG,
	        uint256 total_cargoWeight_in_Kg,
	        uint256 Total_number_of_passenegers_economy_class,
	        uint256 Total_number_of_passenegers_premium_economy_class,
	        uint256 Total_number_of_passenegers_business_class,
	        uint256 Total_number_of_passenegers_first_class
	       
	
	    )
	   
	    external onlyAirlineIndustry {
	        
	        require(registrationContract.isEPA(receiver_EPA), "EPA's address is not valid.");
        require(registrationContract.IATAExists(receiver_IATA), "IATA address is not valid.");
        require(fuelBeginning_in_Kg >= fuelEnding_in_Kg, "Initial fuel should be greater than or equal to final fuel");
        
        
        
        fuel_Consumed_in_Kg = (fuelBeginning_in_Kg - fuelEnding_in_Kg);
        totalWeight_in_Kg =  (total_Passenger_Weight_in_KG + total_cargoWeight_in_Kg);
        total_passenger_FuelBurn_in_Kg = (total_Passenger_Weight_in_KG * fuel_Consumed_in_Kg) / totalWeight_in_Kg;
        

        pre_economy_class_cabin_factor=15;
        business_class_cabin_factor= 4;
        first_class_cabin_factor= 5;
        emissionFactor=316;


        Fuel_Burn_per_Economy_Class_Pax_kg_NM = (1*total_passenger_FuelBurn_in_Kg);
        Fuel_Burn_per_Economy_Class_Pax_kg_D1 = (1*Total_number_of_passenegers_economy_class);
        Fuel_Burn_per_Pre_Economy_Class_Pax_kg_D2= ((pre_economy_class_cabin_factor)*Total_number_of_passenegers_premium_economy_class)/10;
        Fuel_Burn_per_Economy_Class_Pax_kg_D3= ((business_class_cabin_factor)*Total_number_of_passenegers_business_class) ;
        Fuel_Burn_per_Economy_Class_Pax_kg_D4 = ((first_class_cabin_factor)*Total_number_of_passenegers_first_class) ;
        Fuel_Burn_per_Economy_Class_Pax_kg_DF= Fuel_Burn_per_Economy_Class_Pax_kg_D1 + Fuel_Burn_per_Pre_Economy_Class_Pax_kg_D2 + Fuel_Burn_per_Economy_Class_Pax_kg_D3
                                                    +Fuel_Burn_per_Economy_Class_Pax_kg_D4;


        Fuel_Burn_per_Economy_Class_Pax_kg= Fuel_Burn_per_Economy_Class_Pax_kg_NM/Fuel_Burn_per_Economy_Class_Pax_kg_DF;

         Fuel_Burn_per_Premium_Economy_Class_Pax_kg_NM = (pre_economy_class_cabin_factor*total_passenger_FuelBurn_in_Kg);
         Fuel_Burn_per_Premium_Economy_Class_Pax_kg= Fuel_Burn_per_Premium_Economy_Class_Pax_kg_NM/Fuel_Burn_per_Economy_Class_Pax_kg_DF;

        Fuel_Burn_per_Business_Class_Pax_kg_NM = (business_class_cabin_factor*total_passenger_FuelBurn_in_Kg);
        Fuel_Burn_per_Business_Class_Pax_kg = Fuel_Burn_per_Business_Class_Pax_kg_NM/Fuel_Burn_per_Economy_Class_Pax_kg_DF;

        Fuel_Burn_per_First_Class_Pax_kg_NM = (first_class_cabin_factor*total_passenger_FuelBurn_in_Kg);
        Fuel_Burn_per_First_Class_Pax_kg = Fuel_Burn_per_First_Class_Pax_kg_NM/Fuel_Burn_per_Economy_Class_Pax_kg_DF;

        totalFuelBurn_in_Kg=  uint256 ((Fuel_Burn_per_Economy_Class_Pax_kg+Fuel_Burn_per_business_Class_Pax_kg+Fuel_Burn_per_first_Class_Pax_kg));

        Co2_emitted_per_passenger_Economy_class =  ((uint256(emissionFactor) * uint256(Fuel_Burn_per_Economy_Class_Pax_kg))/100)+1;
        Co2_emitted_per_passenger_Premium_Economy_class =  ((uint256(emissionFactor) * uint256(Fuel_Burn_per_Premium_Economy_Class_Pax_kg))/100) +1;
        Co2_emitted_per_passenger_Business_class =  ((uint256(emissionFactor) * uint256(Fuel_Burn_per_Business_Class_Pax_kg))/100) +1;
        Co2_emitted_per_passenger_First_class =  ((uint256(emissionFactor) * uint256(Fuel_Burn_per_First_Class_Pax_kg))/100)+1;
        totalCo2Emitted_in_kg= ((uint256(emissionFactor)* uint256 (fuel_Consumed_in_Kg))/100)+1;



	emit Scope1CarbonEmissionCalculated (fuel_Consumed_in_Kg,  totalWeight_in_Kg, total_passenger_FuelBurn_in_Kg,
                   Fuel_Burn_per_Economy_Class_Pax_kg,Fuel_Burn_per_Premium_Economy_Class_Pax_kg,
                  Fuel_Burn_per_Business_Class_Pax_kg,  Fuel_Burn_per_First_Class_Pax_kg,
                 Co2_emitted_per_passenger_Economy_class, Co2_emitted_per_passenger_Premium_Economy_class,Co2_emitted_per_passenger_Business_class,
                 Co2_emitted_per_passenger_First_class,totalCo2Emitted_in_kg);

}

// Calculate Carbon cost

	event Scope1EmissionCarbonCostCalculated(address receiverEPA,uint256 TotalCo2Emitted_in_kg, uint256 Carbon_Cost_per_TCO2, uint256 Total_Carbon_cost, uint256 		Carbon_cost_per_passeneger_Economy_class,
        uint256 Carbon_cost_per_passeneger_Premium_Economy_class,
        uint256 Carbon_cost_per_passeneger_business_class,
        uint256 Carbon_cost_per_passeneger_first_class);

	function calculateScope1EmissionCarbonCost (address receiverEPA,uint256 TotalCo2Emitted_in_kg, uint256 Carbon_Cost_per_TCO2,uint256 		Total_no_of_passenegers_economy_class,
        uint256 Total_no_of_passenegers_premium_economy_class,
        uint256 Total_no_of_passenegers_business_class,
        uint256 Total_no_of_passenegers_first_class ) public onlyAirlineIndustry{
                            
        Total_Carbon_cost = ((TotalCo2Emitted_in_kg) * (Carbon_Cost_per_TCO2))/1000;
        Carbon_cost_per_passeneger_Economy_class = ((Total_Carbon_cost) / ((Total_no_of_passenegers_economy_class)));
        Carbon_cost_per_passeneger_Premium_Economy_class = ((Total_Carbon_cost) / ((Total_no_of_passenegers_premium_economy_class)));
        Carbon_cost_per_passeneger_business_class = ((Total_Carbon_cost) / ((Total_no_of_passenegers_business_class)));
        Carbon_cost_per_passeneger_first_class = ((Total_Carbon_cost) / ((Total_no_of_passenegers_first_class)));

emit Scope1EmissionCarbonCostCalculated (receiverEPA, TotalCo2Emitted_in_kg,  Carbon_Cost_per_TCO2, Total_Carbon_cost, Carbon_cost_per_passeneger_Economy_class,
 Carbon_cost_per_passeneger_Premium_Economy_class,  Carbon_cost_per_passeneger_business_class,  Carbon_cost_per_passeneger_first_class);

}

event Scope1EmissionPenaltyUpdated (uint256 totalCo2Emitted_in_kg,uint256 ThresholdCO2emission, bool PenaltyStatus);
    
    function updateScope1EmissionPenalty(uint256 ThresholdCO2emission) public {
        require (registrationContract.isEPA(msg.sender)==true,"only EPA can perform this.");
 
    Penalty=false;
        if(totalCo2Emitted_in_kg > ThresholdCO2emission)
         {
            Penalty=true;
        }
    emit Scope1EmissionPenaltyUpdated (totalCo2Emitted_in_kg, ThresholdCO2emission, Penalty);
    }

}

contract Scope2CarbonEmission{
    address payable public Utility_Provider;
    Registration public registrationContract;
    uint256 public Total_Carbon_cost;
    bool Penalty;
   
    

    constructor(address registration) public {
        
        registrationContract = Registration(registration);

        require(registrationContract.Utility_ProviderExists(msg.sender), "Sender not authorized");
        Utility_Provider = payable(msg.sender);
    }
    modifier onlyElectricity_Producer {
        require(registrationContract.Utility_ProviderExists(msg.sender), "Sender not authorized");
        _;
    }

    event Scope2CarbonEmisisonUpdated(address EPA, uint256 Electricty_supplied_in_Kwh, uint256 Total_Co2_emitted_in_Kg, string Fuel_used_for_electricity_production);
    function updateScope2CarbonEmisisonDetails (address EPA, uint256 Electricity_supplied_in_Kwh, string memory Fuel_used_for_electricity_production,
    uint256 Total_Co2_emitted_in_Kg) public onlyElectricity_Producer{

    emit Scope2CarbonEmisisonUpdated(EPA,Electricity_supplied_in_Kwh,Total_Co2_emitted_in_Kg,Fuel_used_for_electricity_production);
    }

    event Scope2CarbonEmisisonCostCalculated(address EPA, uint256 Total_Co2_emitted_in_Kg, uint256 Total_Carbon_cost,uint256 Carbon_Cost_for_Scope2Emission_in_TCO2);
    function CalculateScope2EmissionCarbonCost (address EPA,uint256 Total_Co2_emitted_in_Kg, uint256 Carbon_Cost_for_Scope2Emission_in_TCO2) public onlyElectricity_Producer{

        Total_Carbon_cost = ((Total_Co2_emitted_in_Kg) * (Carbon_Cost_for_Scope2Emission_in_TCO2))/1000;

    emit Scope2CarbonEmisisonCostCalculated(EPA,Total_Co2_emitted_in_Kg,Total_Carbon_cost,Carbon_Cost_for_Scope2Emission_in_TCO2);
    }

event Scope2EmissionPenaltyUpdated (uint256 totalScope2Co2Emitted_in_kg,uint256 ThresholdScope2CO2emission, bool PenaltyStatus);
    
    function updateScope2EmissionPenalty(uint256 totalScope2Co2Emitted_in_kg, uint256 ThresholdScope2CO2emission) public {
        require (registrationContract.isEPA(msg.sender)==true,"only EPA can perform this.");
 
    Penalty=false;
        if(totalScope2Co2Emitted_in_kg > ThresholdScope2CO2emission)
         {
            Penalty=true;
        }
    emit Scope2EmissionPenaltyUpdated (totalScope2Co2Emitted_in_kg, ThresholdScope2CO2emission, Penalty);
    }

}

contract Scope3CarbonEmission{
    address payable public Airport_Authority;
    address payable public Aviation_Fuel_Transporter;
    Registration public registrationContract;
    uint256 public Total_Carbon_cost;
    bool Penalty;
   

    constructor(address registration) public {
        
        registrationContract = Registration(registration);

        require(registrationContract.Airport_AuthorityExists(msg.sender), "Sender not authorized");
        Airport_Authority = payable(msg.sender);
        }
    modifier onlyAirport_Authority {
        require(registrationContract.Airport_AuthorityExists(msg.sender), "Sender not authorized");
        _;
    }

     modifier onlyAviation_Fuel_Transporter {
        require(registrationContract.Aviation_Fuel_TransporterExists(msg.sender), "Sender not authorized");
        _;
    }

    event AirportScope3EmissionUpdated(address EPA, uint256 Total_CO2_emitted_from_Airport_facilities_in_Kg, string Activity_1, string Activity_2,
    string Activity_3);
    function updateAirportScope3Emission (address EPA, uint256 Total_CO2_emitted_from_Airport_facilities_in_Kg, string memory Activity_1, string memory Activity_2,
    string memory Activity_3)
     public onlyAirport_Authority{

    emit AirportScope3EmissionUpdated(EPA, Total_CO2_emitted_from_Airport_facilities_in_Kg, Activity_1,Activity_2,Activity_3 );
    }

    event AirportScope3CarbonCostCalculated (address EPA, uint256 Total_CO2_emitted_from_Airport_facilities_in_Kg, uint256 Total_Carbon_cost,uint256 Carbon_Cost_for_AirportEmission_in_TCO2);
    function CalculateAirportScope3CarbonCost(address EPA, uint256 Total_CO2_emitted_from_Airport_facilities_in_Kg, uint256 Carbon_Cost_for_AirportEmission_in_TCO2) public onlyAirport_Authority{

        Total_Carbon_cost = ((Total_CO2_emitted_from_Airport_facilities_in_Kg) * (Carbon_Cost_for_AirportEmission_in_TCO2))/1000 + 1;
    emit AirportScope3CarbonCostCalculated (EPA, Total_CO2_emitted_from_Airport_facilities_in_Kg,  Total_Carbon_cost, Carbon_Cost_for_AirportEmission_in_TCO2);
    }

    event FuelTransportationScope3EmisisonUpdated(address EPA, string Fuel_Type, uint256 amount_of_fuel_supplied, uint256 Total_CO2_emitted_from_Fuel_TransportationandStorage_in_Kg);
    function updateFuelTransportationScope3Emisison(address EPA, string memory Fuel_Type, uint256 amount_of_fuel_supplied, uint256 Total_CO2_emitted_from_Fuel_TransportationandStorage_in_Kg) public onlyAviation_Fuel_Transporter{
    
    emit FuelTransportationScope3EmisisonUpdated(EPA, Fuel_Type, amount_of_fuel_supplied,Total_CO2_emitted_from_Fuel_TransportationandStorage_in_Kg);
    }
    event FuelTransportationScope3CarbonCostCalculated(address EPA, uint256 Total_CO2_emitted_from_Fuel_TransportationandStorage_in_Kg, uint256 Carbon_Cost_for_Fuel_TransportationandStoragetEmission_in_TCO2, uint256 Total_Carbon_cost);
    function calculateFuelTransportationCarbonCost(address EPA, uint256 Total_CO2_emitted_from_Fuel_TransportationandStorage_in_Kg, 
    uint256 Carbon_Cost_for_Fuel_TransportationandStoragetEmission_in_TCO2) public onlyAviation_Fuel_Transporter{

        Total_Carbon_cost = ((Total_CO2_emitted_from_Fuel_TransportationandStorage_in_Kg) * (Carbon_Cost_for_Fuel_TransportationandStoragetEmission_in_TCO2))/1000 + 1;

    emit FuelTransportationScope3CarbonCostCalculated (EPA, Total_CO2_emitted_from_Fuel_TransportationandStorage_in_Kg,Carbon_Cost_for_Fuel_TransportationandStoragetEmission_in_TCO2,Total_Carbon_cost);
    }      
    
event Scope3EmissionPenaltyUpdated (uint256 total_Airport_Facility_Scope3_Co2Emitted_in_kg, uint256 total_Fuel_Storageandtransportation_Scope3_Co2Emitted_in_kg, uint256 Threshold_Airport_Facility_Scope3_CO2emission, uint256 Threshold_Fuel_TransportationandStorage_Scope3_CO2emission, bool PenaltyStatus);
    
    function updateScope3EmissionPenalty(uint256 total_Airport_Facility_Scope3_Co2Emitted_in_kg, uint256 total_Fuel_Storageandtransportation_Scope3_Co2Emitted_in_kg, uint256 Threshold_Airport_Facility_Scope3_CO2emission, uint256 Threshold_Fuel_TransportationandStorage_Scope3_CO2emission) public {
        require (registrationContract.isEPA(msg.sender)==true,"only EPA can perform this.");
 
    Penalty=false;
        if(total_Airport_Facility_Scope3_Co2Emitted_in_kg > Threshold_Airport_Facility_Scope3_CO2emission)
         {
            Penalty=true;
        }

        if(total_Fuel_Storageandtransportation_Scope3_Co2Emitted_in_kg > Threshold_Fuel_TransportationandStorage_Scope3_CO2emission)
         {
            Penalty=true;
        }
    emit Scope3EmissionPenaltyUpdated (total_Airport_Facility_Scope3_Co2Emitted_in_kg, total_Fuel_Storageandtransportation_Scope3_Co2Emitted_in_kg, Threshold_Airport_Facility_Scope3_CO2emission, Threshold_Fuel_TransportationandStorage_Scope3_CO2emission, Penalty);
    }
}

contract CarbonOffset {
    address payable Carbon_offset_provider;
    Registration public registrationContract;
    bool Offset_Required;
    bool Carbon_Credit;
    uint256 public CarbonOffsetamount;
    uint256 public CarbonCreditamount;

    constructor(address registration) public {
        registrationContract = Registration(registration);

        require(registrationContract.Carbon_offset_providerExists(msg.sender), "Sender not authorized");
        Carbon_offset_provider = payable(msg.sender);
    }

    modifier onlyCarbon_offset_provider {
        require(registrationContract.Carbon_offset_providerExists(msg.sender), "Sender not authorized");
        _;
    }

  event CarbonOffsetandCreditStatusUpdated (
    uint256 Baseline_Carbon_Emissions,
    uint256 Actual_Carbon_Emission,
    uint256 CarbonOffsetamount,
    uint256 CarbonCreditamount,
    string Carbon_offset_project,
    bool Offset_RequiredStatus,
    bool Carbon_CreditStatus
);

function updateCarbonOffsetandCreditStatus (
    uint256 Baseline_Carbon_Emissions,
    uint256 Actual_Carbon_Emission, string memory Carbon_offset_project) public onlyCarbon_offset_provider {


    if (Actual_Carbon_Emission > Baseline_Carbon_Emissions) {
        CarbonOffsetamount = Actual_Carbon_Emission - Baseline_Carbon_Emissions;
        Offset_Required = true;
        Carbon_Credit = false;

    } else if (Baseline_Carbon_Emissions > Actual_Carbon_Emission) {
        
        CarbonCreditamount = Baseline_Carbon_Emissions - Actual_Carbon_Emission;
        Carbon_Credit = true;
        Offset_Required = false;
    } else {
        CarbonOffsetamount = 0;
        CarbonCreditamount=0;
        Offset_Required = false;
        Carbon_Credit = false;
    }

    emit CarbonOffsetandCreditStatusUpdated (Baseline_Carbon_Emissions, Actual_Carbon_Emission, CarbonOffsetamount, CarbonCreditamount, Carbon_offset_project,Offset_Required,Carbon_Credit);
}


}

