
```
Ext.define('User', {
    extend: 'Ext.data.Model',
    fields: ['skRegionPk','regionId','regionName'],
    proxy : {
        type: 'dwr',
        //assume that we have dwr function getTestGrid(storeParameters a,Integer b,Integer c)
        //first one goes automatically it includes start,limit,page and other store parameters
        //second and third are optional we pass them through dwrParams as an array
        dwrFunction : {
        	read : WTGEventInterface.getRegionList,
        	create : WTGEventInterface.addRegion,
        	update : WTGEventInterface.updateRegion,
        	delete : WTGEventInterface.deleteRegion
        },
        dwrParams : [],
        reader : {
        	type : 'json',
            root : 'data',
            totalProperty:'totalCount'
        }
    }
});

Store = Ext.create('Ext.data.Store', {
    requiers : ['Ext.ux.DwrProxy'],
    model: 'User'
});
```