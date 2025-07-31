import 'package:flutter/material.dart';
import 'package:hdfc_flutter_widgets/common/secondary_button.dart';
import 'package:hdfc_flutter_widgets/common/menu_button.dart';
import 'package:hdfc_flutter_widgets/event_card/common/payment_status.dart';
import 'package:hdfc_flutter_widgets/event_card/common/logo.dart';
import 'package:hdfc_flutter_widgets/event_card/common/smart_info_card.dart';
import 'package:hdfc_flutter_widgets/event_card/common/primary_detail.dart';

class EventCardActionItem {
  final String title;
  final VoidCallback onTap;
  final bool isPrimary;

  EventCardActionItem({required this.title, required this.onTap, this.isPrimary = true});
}

/// A reusable and responsive compact event card widget.
/// Use this to show payment/event-related information in a summarized format.
class CompactEventCard extends StatelessWidget {
  final List<EventCardActionItem> actionItems;

  /// Path to the event icon (usually an SVG).
  final String prefixIconPath;

  /// Background color for event icon.
  final Color prefixIconColor;

  /// Path to the biller logo/icon.
  final String suffixIconPath;

  /// Event name to display.
  final String title;

  final String subTitle;

  /// Label text for smart pay status (e.g. "Enabled", "Disabled").
  final String descriptionText;

  /// Icon path for smart pay status.
  final String descriptionIconPath;

  /// Total amount to be paid/shown.
  final double amount;

  /// Status string for the bill (e.g. "Paid", "Overdue").
  final String paymentStatus;

  /// Bill status text background color.
  final Color paymentStatusBackgroundColor;

  /// Bill status text color.
  final Color paymentStatusTextColor;

  final String eventDateWithLabel;

  final String menuButtonIconPath;

  const CompactEventCard({
    super.key,
    required this.prefixIconPath,
    required this.suffixIconPath,
    required this.descriptionText,
    required this.descriptionIconPath,
    required this.amount,
    required this.paymentStatus,
    required this.paymentStatusBackgroundColor,
    required this.paymentStatusTextColor,
    required this.title,
    required this.prefixIconColor,
    required this.actionItems,
    required this.subTitle,
    required this.eventDateWithLabel,
    required this.menuButtonIconPath,
  });

  /// Top container decoration
  BoxDecoration _topContainerDecoration(BuildContext context) => BoxDecoration(
    color: Colors.lightBlue[50],
    border: Border.all(color: Theme.of(context).primaryColor, width: 1.0),
    borderRadius: const BorderRadius.only(
      topLeft: Radius.circular(20),
      topRight: Radius.circular(20),
    ),
  );

  /// Bottom container decoration
  BoxDecoration _bottomContainerDecoration(BuildContext context) => BoxDecoration(
    color: Colors.white,
    borderRadius: const BorderRadius.only(
      bottomLeft: Radius.circular(8),
      bottomRight: Radius.circular(8),
    ),
    border: Border(
      left: BorderSide(color: Theme.of(context).primaryColor, width: 1),
      right: BorderSide(color: Theme.of(context).primaryColor, width: 1),
      bottom: BorderSide(color: Theme.of(context).primaryColor, width: 1),
    ),
  );

  @override
  Widget build(BuildContext context) {
    final EventCardActionItem? primaryAction = actionItems.isNotEmpty ? actionItems.first : null;
    final List<EventCardActionItem> secondaryAction = actionItems.length > 1
        ? actionItems.sublist(1)
        : [];

    return LayoutBuilder(
      builder: (context, constraints) {
        return Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // Top section: Event details and smart pay
            Container(
              decoration: _topContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 15),
              child: Row(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Expanded(
                    child: PrimaryDetail(
                      title: title,
                      prefixIconPath: prefixIconPath,
                      prefixIconBackgroundColor: prefixIconColor,
                      descriptionIconPath: descriptionIconPath,
                      descriptionText: descriptionText,
                      subtitle: subTitle,
                    ),
                  ),
                  Logo(svgPath: suffixIconPath, size: 50),
                ],
              ),
            ),

            // Bottom section: Payment info + actions
            Container(
              decoration: _bottomContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 15),
              child: Column(
                children: [
                  // Amount + Bill status + Date pill
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      Expanded(
                        child: Row(
                          mainAxisSize: MainAxisSize.min,
                          children: [
                            Flexible(
                              child: Text(
                                '₹ ${amount.toStringAsFixed(2)}',
                                style: const TextStyle(fontSize: 15, fontWeight: FontWeight.bold),
                                // overflow: TextOverflow.ellipsis,
                                // maxLines: 2,
                              ),
                            ),
                            const SizedBox(width: 10),
                            Flexible(
                              child: PaymentStatus(
                                status: paymentStatus,
                                borderTextColor: paymentStatusTextColor,
                                backgroundColor: paymentStatusBackgroundColor,
                              ),
                            ),
                          ],
                        ),
                      ),
                      SizedBox(width: 2),
                      Flexible(child: SmartInfoCard(text: eventDateWithLabel)),
                    ],
                  ),
                  const SizedBox(height: 10),

                  // Bottom actions
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    // crossAxisAlignment: CrossAxisAlignment.stretch,
                    children: [
                      if (primaryAction != null)
                        Expanded(
                          child: SecondaryButton(
                            title: primaryAction.title,
                            onTap: primaryAction.onTap,
                          ),
                        ),

                      const SizedBox(width: 10),

                      if (secondaryAction.isNotEmpty)
                        MenuButton(
                          options: secondaryAction.map((e) => e.title.toString()).toList(),
                          onSelect: (selectedTitle) {
                            final EventCardActionItem selected = secondaryAction.firstWhere(
                              (element) => element.title == selectedTitle,
                            );
                            selected.onTap();
                          },
                          iconPath: menuButtonIconPath,
                        ),
                    ],
                  ),
                ],
              ),
            ),
          ],
        );
      },
    );
  }
}
