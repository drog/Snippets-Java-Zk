
# Busqueda de un componentes recursivamente

```java
public static Component findComponentInParent(Class<?> zclass, Component component) {
		if(component!=null && component.getParent()!=null){
			if(zclass.isInstance(component.getParent())){
				return component.getParent();
			}else{
				return findComponentInParent(zclass, component.getParent());
				}
			}
		return null;
	}
	
public static List<Component> searchAllComponentsInChildren(Class<?> zclass, Component component){
  List<Component> listComponents = new ArrayList<Component>();
  return searchAllComponentsInChildren(zclass, component, listComponents);
}
	
private static List<Component> searchAllComponentsInChildren(Class<?> zclass, Component component, List<Component> listComponents) {
  List<Component> components = listComponents;
  if(component!=null && CollectionUtils.isNotEmpty(component.getChildren())){
    for(Object object : component.getChildren()){
      if(zclass.isInstance(object)){
        components.add((Component) object);
      }else if(object instanceof Component){
        components = searchAllComponentsInChildren(zclass, (Component) object, components);
      }
    }
  }
  return listComponents;
}
```


# [Clausula In mayor a 1000 elementos en Oracle](https://stackoverflow.com/questions/19002792/why-oracle-in-clause-has-limit-of-1000-only-for-static-data)
```java
public static final Integer ORACLE_MAX_VALUES_SUPPORTED_IN_CLAUSE = 1000;

public static <T> List<List<T>> chopped( List<T> list, final int max ) {
		List<List<T>> parts = new ArrayList<List<T>>();
		final int total = list.size();
		for ( int i = 0; i < total; i += max ) {
			parts.add( new ArrayList<T>( list.subList( i, Math.min( total, i + max ) ) ) );
		}
		return parts;
	}
  
@SuppressWarnings ( "rawtypes" )
	public static <E extends Comparable> JPAQuery divideListNotIn( JPAQuery query, List<E> listaIds, ComparableExpressionBase<E> path, Integer max ) {
		if ( listaIds != null ) {
			List<List<E>> parts = chopped( listaIds, max );
			BooleanExpression criteria = null;
			for ( List<E> pp : parts ) {
				criteria = criteria == null ? path.notIn( pp ) : criteria.or( path.notIn( pp ) );
			}
			query.where( criteria );
		}
		return query;
	}
```


# Propiedades Tomcat

```
-Dprops.path="C:\properties" -Xms2048m -Xmx2048m -XX:PermSize=2048m -XX:MaxPermSize=2048m -XX:+UseParallelGC -XX:+CMSClassUnloadingEnabled -Ddb.type=postgres
```
