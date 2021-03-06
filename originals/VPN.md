
## Description

Rackspace Hosting - VPN Setup Template. http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_VPN.html

#### Metadata

 * **Comments**: Generated by Ansible
 * **Version**: v0.1.2

## Parameters

 * **CustomerIP** - The IP address of the Customer Endpoint, in CIDR notation
  * Default: `0.0.0.0`
  * Constraint: `Must be a valid CIDR range of the form x.x.x.x`
 * **DefaultStaticRoute** - This is the internal subnet IP Cidr on the customer side. Leave the default value if you do not intend to set a static route.
  * Default: `127.0.0.1/32`
  * Constraint: `Must be a valid CIDR range of the form x.x.x.x/x`
 * **Environment** - Application environment for which this network is being created. e.g. Development/Production.
  * Default: `Development`
 * **ExistingCGWId** - Leave blank unless you already have an existing CGW attached in the VPC you're creating this VPN Connection in.
  * Default: ``
 * **ExistingVGWId** - Leave blank unless you already have an existing VGW attached in the VPC you're creating this VPN Connection in.
  * Default: ``
 * **PropagateRoutesTo** - A comma separated list of route tables you would like to propagate the VPN Route to.
  * Default: ``
 * **VPCID** - Select Virtual Private Cloud ID

## Conditions

 * **CreateNewCGW** - `{u'Fn::Equals': [{u'Ref': u'ExistingCGWId'}, u'']}`
 * **CreateNewVGW** - `{u'Fn::Equals': [{u'Ref': u'ExistingVGWId'}, u'']}`
 * **PropagateRoutes** - `{u'Fn::And': [{u'Fn::Not': [{u'Fn::Equals': [{u'Fn::Select': [u'0', {u'Ref': u'PropagateRoutesTo'}]}, u'']}]}, {u'Fn::Equals': [{u'Ref': u'ExistingVGWId'}, u'']}]}`
 * **SetStaticRoute** - `{u'Fn::Not': [{u'Fn::Equals': [{u'Ref': u'DefaultStaticRoute'}, u'127.0.0.1/32']}]}`

## Resources

 * **AttachVpnGateway** - `AWS::EC2::VPCGatewayAttachment`
 * **CustomerGateway** - `AWS::EC2::CustomerGateway`
 * **VPNConnection** - `AWS::EC2::VPNConnection`
 * **VPNConnectionRoute** - `AWS::EC2::VPNConnectionRoute`
 * **VPNGateway** - `AWS::EC2::VPNGateway`
 * **VPNRoutePropagation** - `AWS::EC2::VPNGatewayRoutePropagation`

## Outputs

 * **outputCustomerGatewayId** - `{u'Ref': u'CustomerGateway'}`
 * **outputVirtualPrivateGatewayId** - `{u'Ref': u'VPNGateway'}`