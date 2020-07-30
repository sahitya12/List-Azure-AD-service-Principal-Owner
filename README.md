# List-Azure-AD-service-Principal-Owner

Connect-AzureAD
$results = @()
Get-AzureADApplication -All $true | %{  
                             $app = $_


                             $owner = Get-AzureADApplicationOwner -ObjectId $_.ObjectID -Top 1 
                             $ServicePrincipalId = (Get-AzureADServicePrincipal -Top 1).ObjectId 


                             $app |
                                %{ 
                                    $results += [PSCustomObject] @{
                                            DisplayName = $app.DisplayName; 
                                            ObjectID =  $app.ObjectID;
                                            Owners = $owner.UserPrincipalName
                                    }
                                    }
                            }

$results | FT -AutoSize 
