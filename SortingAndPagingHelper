    /// <summary>
    /// Extension para ordenar y paginar
    /// </summary>
    public static class SortingAndPagingHelper
    {
        public static IEnumerable<TSource> SortingAndPaging<TSource>(this IEnumerable<TSource> source, PaginatorModel paginationOrder)
        {
            int PageSelected = paginationOrder.StartNumber ?? 0;
            int PageSize = paginationOrder.PageSize ?? 10;
            string columnOrder = string.IsNullOrEmpty(paginationOrder.ColumnOrder) ? "Name" : paginationOrder.ColumnOrder;

            // Gets the coloumn name that sorting to be done on
            PropertyInfo propertyInfo = source.GetType().GetGenericArguments()[0].GetProperty(columnOrder)
                                        ?? source.GetType().GetGenericArguments()[0].GetProperty("Name");

            // sorts by ascending if sort criteria is Ascending otherwise sorts descending
            return paginationOrder.SortDirection == SortDirectionCode.Desc ? source.OrderByDescending(x => propertyInfo.GetValue(x, null)).Skip(PageSelected * PageSize).Take(PageSize)
                               : source.OrderBy(x => propertyInfo.GetValue(x, null)).Skip(PageSelected * PageSize).Take(PageSize);
        }
    }
    
     public class PaginatorModel
    {
        /// <summary>
        /// campo de orden
        /// </summary>
        public string ColumnOrder { get; set; }

        /// <summary>
        /// Tamaño de la pagina
        /// </summary>
        public int? PageSize { get; set; }

        /// <summary>
        /// Criterio de orden asc o desc
        /// </summary>
        public SortDirectionCode? SortDirection { get; set; }

        /// <summary>
        /// Numero de inicio de paginacion
        /// </summary>
        public int? StartNumber { get; set; }
    }
